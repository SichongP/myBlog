---
title: How to run snakemake pipeline on HPC
author: Sichong Peng
date: '2019-10-17'
slug: how-to-run-snakemake-pipeline-on-hpc
categories:
  - Workflow
tags:
  - bioinformatics
  - Workflow
image:
  caption: ''
  focal_point: ''
---

## Why use Snakemake on HPC
Snakemake is a handy workflow manager written in Python. It handles workflow based on predefined job dependencies. One of the great features of Snakemake is that it can manage a workflow on both a standalone computer, or a clustered HPC system. HPC, or "cluster" as it's often referred to, requires additional considerations. 

On HPC, all computing jobs should be submitted to "compute nodes" through a workload manager (for example, Slurm). Running jobs on "heaed nodes", or log-in nodes, is a big no-no: doing so risks exhausting computing resources of head node computer (which is very limited) and slowing down everyone else on that same head node.

File system is another thing that requires consideration when computing on HPC. Many HPC systems use NFS (Network File System) to have storage system accessible to all computing and head nodes. But some HPC systems also have dedicated local storage for each compute node. This is to help offload I/Os from major storage drives when users are running jobs with intensive I/O. It is important that users make use of these local storage spaces, as well as clean up their temporary files.

Below I will show how to achieve responsible computing on HPC with a few tweaks to your Snakemake workflow.

## How to run snakemake on HPC
Snakemake natively supports managing job submission on HPC. Take a look at their [documentation here](https://snakemake.readthedocs.io/en/stable/executable.html#cluster-execution). 

Let's assume I have a Snakefile with following minimal rules:
```{python}
rule all:
    input: "RawData/Sample.fastq.gz"

rule compressFASTQ:
    input: "RawData/Sample.fastq"
    output: "RawData/Sample.fastq.gz"
    shell:
     """
     gzip {input}
     """
```
To execute this workflow locally, we can simply invoke `snakemake -s path/to/Snakefile` (or `snakemake` if you're in the same directory as `Snakefile`).

Now if we want to run this on HPC on compute nodes, Snakemake allows us to do so by:
```
snakemake -s Snakefile --cluster 'sbatch -t 60 --mem=2g -c 1'
```
In the above command, we use `--cluster` to hand Snakemake a command that it can use to submit a job script. Snakemake creates a job script for each job to be run and uses this command to submit that job to HPC. That simple!
Notice that here we use `sbatch` because it's the command you would use to submit a shell script on HPC managed by Slurm. Replace this with `qsub` commands if your HPC uses SGE. 

## Decorate your job submission

### Claim different resources based on rules

Now suppose we have a slightly more complicated workflow:
```{python}
samples = ['sample1', 'sample2', 'sample3', 'sample4']
rule all:
    input: expand("Alignment/{sample}.bam", sample = samples)

rule downloadFASTQ:
    output: "RawData/{sample}_1.fastq.gz", "RawData/{sample}_2.fastq.gz"
    shell:
     """
     ascp username@host:path/to/file/{wildcards.sample} RawData/
     """

rule mapFASTQ:
    input: 
        f1 = "RawData/{sample}_1.fastq.gz", 
        f2 ="RawData/{sample}_2.fastq.gz", 
        ref = "Ref/ref.fa"
    output: temp("Alignment/{sample}.sam")
    shell:
     """
     bwa mem -R "@RG\\tID:{wildcards.sample}\\tSM:{wildcards.sample}" {input.ref} {input.f1} {input.f2} > {output}
     """

rule convertSAM:
    input: "Alignment/{sample}.sam"
    output: "Alignment/{sample}.bam"
    shell:
     """
     samtools view -bh {input} > {output}
     """
```

Now in this workflow, different jobs require different computing resources: `mapFASTQ` probably requires more RAM than `downloadFASTQ` does. And more threads would probably speed up `mapFASTQ` but change little to `downloadFASTQ`. Using `--cluster` like shown above will cause all jobs to request same amount of resources from HPC. How can we make Snakemake request different amount of resources based on each job?

This can be easily achieved by two ways:

1. Define resources in rule parameters:

The string following `--cluster` can access all variables within a rule like we could do in a shell command within a rule. For example, we can define `rule mapFASTQ` shown above as this instead:

```{python}
rule mapFASTQ:
    input: 
        f1 = "RawData/{sample}_1.fastq.gz", 
        f2 ="RawData/{sample}_2.fastq.gz", 
        ref = "Ref/ref.fa"
    output: temp("Alignment/{sample}.sam")
    threads: 8
    params: time = 120, mem = "8g"
    shell:
     """
     bwa mem -@ {threads} -R "@RG\\tID:{wildcards.sample}\\tSM:{wildcards.sample}" {input.ref} {input.f1} {input.f2} > {output}
     """
```
And then we can revoke the workflow by:
```
snakemake -s Snakefile --cluster 'sbatch -t {params.time} --mem={params.mem} -c {threads}'
```
Notice that you must define these params for all rules or you will get an error when Snakemake tries to submit a job from a rule that doesn't have one or more of these params defined.

Another more convinient way involves using a separate cluster config file:

2. Define resources in cluster.config:

Instead of putting parameters for cluster submission into each individual rule, you can write a separate config file that contains these parameters:

*cluster.yaml*:
```
__default__:
  partition: "high"
  cpus: "{threads}"
  time: 60
  mem: "2g"

mapFASTQ:
  mem: "8g"
  time: 120
  
convertSAM:
  mem: "4g"
```
This file defines dafault parameters Snakemake will use for job submissions for all rules, *unless* they are overridden by specific parameters defined below.

Now in our rule definition, we only need to specify `threads`:

```{python}
rule mapFASTQ:
    input: 
        f1 = "RawData/{sample}_1.fastq.gz", 
        f2 ="RawData/{sample}_2.fastq.gz", 
        ref = "Ref/ref.fa"
    output: temp("Alignment/{sample}.sam")
    threads: 8
    shell:
     """
     bwa mem -@ {threads} -R "@RG\\tID:{wildcards.sample}\\tSM:{wildcards.sample}" {input.ref} {input.f1} {input.f2} > {output}
     """
```

The reason I keep `threads` in rule definition is because when running on a local machine Snakemake can still utilize this paramter for multi-threading

Then we can revoke by:

```
snakemake -s Snakefile --cluster-config cluster.yaml --cluster 'sbatch -t {cluster.time} --mem={cluster.mem} -c {cluster.cpus}'
```

### Redirect cluster output
When running a job on cluster, stdout and stderr are not immediately obvious. Slurm managed systems redirect them to `slurm-JOBID.txt` in working directory by default. This can be hard to tracked down when you're using Snakemake to manage more than a few dozen jobs. Luckily, with Snakemake this can be very easily changed. Let's modify out `cluster.yaml` file:

```
__default__:
  partition: "high"
  cpus: "{threads}"
  time: 60
  mem: "2g"
  output: "logs_slurm/{rule}.{wildcards}.out"
```

And then we revoke Snakemake by:

```
snakemake -s Snakefile --cluster-config cluster.yaml --cluster 'sbatch -t {cluster.time} --mem={cluster.mem} -c {cluster.cpus} -o {cluster.output} -e {cluster.output}'
```

This will redirect stdout and stderr of every job to their corresponding log files named as by rule and wildcards (eg. `downloadFASTQ.sample1.out`) under `logs_slurm` directory. If a particular job fails, it's super easy to find its log file!

### Email notification when a job fails
Often times it's desirable to know when a job fails. You can have cluster notify you by email simply by modifying `cluster.yaml` to include cluster params for email notifications. For example:

```
__default__:
  partition: "high"
  cpus: "{threads}"
  time: 60
  mem: "2g"
  output: "logs_slurm/{rule}.{wildcards}.out"
  email: "user@host.com"
  email_type: "FAIL"
```

And then revoke Snakemake with:
```
snakemake -s Snakefile --cluster-config cluster.yaml --cluster 'sbatch -t {cluster.time} --mem={cluster.mem} -c {cluster.cpus} -o {cluster.output} -e {cluster.output} --mail-type {cluster.email_type} --mail-user {cluster.email}'
```

### Put Snakemake command in a "scheduler" script
Evidently, as our cluster config parameters grow, the command to revoke Snakemake also grows and it becomes tedious to type every time. To avoid this, you can simply put this command in a sbtach script like so:

*scheduler.sh*
```
#! /bin/bash -login
#SBATCH -J scheduler
#SBATCH -t 7-00:00:00
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -c 1  
#SBATCH -p high
#SBATCH --mem=2gb
#SBATCH --mail-type=ALL
#SBATCH --mail-user=user@host.com

cd /path/to/snakemake/piepeline

mkdir -p logs_slurm
snakemake -s Snakefile --cluster-config cluster.yaml --cluster 'sbatch -t {cluster.time} --mem={cluster.mem} -c {cluster.cpus} -o {cluster.output} -e {cluster.output} --mail-type {cluster.email_type} --mail-user {cluster.email}'
```
And then submit this script to cluster using `sbatch scheduler.sh`. Then all you need to do is sit back and wait for it to finish (or error out).

## Best practice on cluster
(To be updated)