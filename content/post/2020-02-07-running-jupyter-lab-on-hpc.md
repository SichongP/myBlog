---
title: Running Jupyter Lab on HPC
author: Sichong Peng
date: '2020-02-07'
slug: running-jupyter-lab-on-hpc
categories:
  - Workflow
tags:
  - bioinformatics
image:
  caption: ''
  focal_point: ''
draft: true
---

For years I have been sticking with R and RStudio, primarily because RStudio's useful and user-friendly GUI design (and my own comfort with Tidyverse). Indeed, my biggest complain against Jupyter Notebook whenever somebody introduced it to me was its bare-bone functionality. Until I discovered [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/)!

I have been experimenting with Jupyter Lab and migrating some of my work there. And I'm happy to report that I'm fully ready to jump the ship and join team Jupyter at this point!

Below I'll share my Jupyter Lab set up on my HPC. 

## Install Jupyter Lab 

We are gonna use `conda` to install jupyter lab in a separate env. Conda makes it easy to manage pacakges and dependencies. As you will undoubtedly need many packages for your analysis (`numpy`, `scipy`, `pandas`, `matplotlib`, `scikit-learn`, to name a few), Conda will definitely save you a tremendous amount of headache. Checkout [Conda](https://www.anaconda.com/) for more details.

To install Jupyter Lab into a new conda env, run the following code:
```
conda create -n jupyter -c conda-forge jupyter-lab nodejs
```

We are installing `node.js` along with Jupyter Lab here because it's a dependancy for Jupyter Lab Extensions, a set of tools that make JL extremely powerful.


## Start a Jupyter Lab instance remotely

Since we are on HPC, we would like to avoid running anything on head nodes. So let's request an interactive node for our server:
```
srun -t 08:00:00 -p bmh --mem=8g --pty bash
```

Here I'm requesting 8 hours and 8g of RAM for this job on a queue called `bmh`. I generally find 8g enough for my work but obviously this depends on your specific needs. The queue `bmh` is cluster specific but generally you want to be on a queue where your job won't be interupted or terminated by other jobs.

Now once you're logged on a compute node, take a note of the node you're on. This is generally indicated at your command prompt:
```
pengsc@bm3:~$ 
```
This indicates that I'm on a node called "bm3". 

Now we can activate our jupyter env and start a Jupyter Lab instance:
```
conda activate jupyter
jupyter-lab --port 8888 --no-browser
```

Here we're telling jupyter-lab to start an instance and forward traffic to port `8888`. `--no-browser` tells jupyter-lab to not open a page in browser, which is the default setting, since we don't have a browser GUI on cluster.

Now that Jupyter Lab is up and running on a compute node `bm3`, we go to a local terminal:
```
ssh -t -t username@host -L 8888:localhost:8888 ssh bm3 -L 8888:localhost:8888
```

This command is a little confusing so let's break it down:
- The first `ssh` starts a tunnel between our local machine and remote host (head node)
- `-t -t` forces a tty (terminal) on head node. This is required to tunnel data back to head node from compute node
- `username@host` this is your login credential
- `-L 8888:localhost:8888` This directs ssh to tunnel traffic from port 8888 on head node to port 8888 on local machine. If the port on either end is used by other programs, you can simply change this to a different number.
- The second `ssh` starts a tunnel between head node and compute node
- `bm3` is the compute node our jupter-lab is currently running on
- `-L 8888:localhost:8888` This directes ssh to tunnel traffic from port 8888 on cmpute node bm3 to head node

Now we can head on to our browser at `localhost:8888`. This should open up a page where Jupyter Lab resides!

## Now time to automate it!

Starting a jupyter lab involves a lot of steps and I found myself constantly referring to notes or google. So I decided to automate this!

```
#! /bin/bash -login
#SBATCH -J JupyterLab
#SBATCH -t 08:00:00
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -c 1
#SBATCH -p bmh
#SBATCH --mem=6gb
#SBATCH --output=/home/%u/jupyter.log
conda activate jupyter
echo "Connect to jupyter lab server with following command:"
echo "ssh -t -t pengsc@farm.cse.ucdavis.edu -L 8888:localhost:8888 ssh ${SLURMD_NODENAME} -L 8888:localhost:8888"
echo "Then connect to Jupyter Lab in your browser as localhost:8888"
echo "Terminate this job by:"
echo "1. Shut down server from Jupyter Lab"
echo "2. scancel $SLURM_JOBID"
jupyter-lab --port 8888 --no-browser
echo "Server terminated..."
exit
```

Put above code in a scipt and adjust `#SBATCH` parameters according to your specific needs. Now everytime you need to start up a jupyter lab instance, simply run this script! You will find a log file at `~/jupyter.log` with content like this:

```
==========================================
SLURM_JOB_ID = 19502530
SLURM_NODELIST = bm8
==========================================
Connect to jupyter lab server with following command:
ssh -t -t pengsc@farm.cse.ucdavis.edu -L 8888:localhost:8888 ssh bm8 -L 8888:localhost:8888
Then connect to Jupyter Lab in your browser as localhost:8888
Terminate this job by:
1. Shut down server from Jupyter Lab
2. scancel 19502530

```
This tells you which command to run on your local terminal to connect to jupyter server, as well as how to properly terminate this instance.

If you find copy-pasting commands still too much trouble, you can also make a bash function in `~/.bashrc`:

```
function jupyter_server()
{ #use node as argument
        ssh -t -t user@host -L 8888:localhost:8888 ssh $1 -L 8888:localhost:8888
}
```
And then you just need to figure out the name of compute node your jupyter lab instance is running on and:
```
jupyter_server name
```
