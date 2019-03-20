---
title: Split a FASTA record by Ns
author: Sichong Peng
date: '2019-03-20'
slug: split-a-fasta-record-by-ns
categories:
  - Python
tags:
  - Python
  - bioinformatics
  - FASTA
image:
  caption: ''
  focal_point: ''
---

I want to split sequences in a fasta file at Ns.  

Here is what an example file looks like:
```
>1_name
ACGTTGCGGCATTCGATCGACGATCGATGCAAACGGTCACGGACTGACTGT
ACACACGTAGCAGCATCAGCATNNNNNNNNNNNNNNNNNNNNGTTGGACGG
NNNNNNNNNNNNGGTGACACACGAGATATATFAGATCAACGTAAGGGATGA
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
AGTCGCTAGCATGCATGGCATATACGCGATCGATTCGATAGCTAGCGNNNN
>2_name
ACGTTGCGGCATTCGATCGACGATCGATGCAAACGGTCACGGACTGACTGT
ACACACGTAGCAGCATCAGCATATTCGATGGCATCGATACCGGTTGGACGG
NNNNNNNNNNNNGGTGACACACGAGATATATFAGATCAACGTAAGGGATGA
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
AGTCGCTAGCATGCATGGCATATACGCGATCGATTCGATAGCTAGCGNNNN
```
There are two common formats for FASTA files:  
- Single line FASTA  
    Each record consists of two line: a name line (starts with ">") and a sequence line.
- Multiline FASTA  
    Each records consists of multiple lines, First line is a name line (starts with ">"), followed by multiple lines of sequences.
  
Here I assume I'm dealing with multiline FASTA because if a script can work with multiline fasta, it's generally easy to make it work with single line files.

Here is how I approach it:


```python
import sys

with open('test','r') as f:
    seq = []
    for line in f:
        if line.startswith(">"):
            if seq: #seq not empty, process it
                trim = '\n'.join(''.join(seq).replace("N"," ").split())
                print(trim)
                seq = []
            print(line.strip())
        else:
            #Read lines into a single seq
            seq.append(line.strip())
    if seq: #seq not empty, process it
                trim = '\n'.join(''.join(seq).replace("N"," ").split())
                print(trim)
                seq = []
```

    >1_name
    ACGTTGCGGCATTCGATCGACGATCGATGCAAACGGTCACGGACTGACTGTACACACGTAGCAGCATCAGCAT
    GTTGGACGG
    GGTGACACACGAGATATATFAGATCAACGTAAGGGATGA
    AGTCGCTAGCATGCATGGCATATACGCGATCGATTCGATAGCTAGCG
    >2_name
    ACGTTGCGGCATTCGATCGACGATCGATGCAAACGGTCACGGACTGACTGTACACACGTAGCAGCATCAGCATATTCGATGGCATCGATACCGGTTGGACGG
    GGTGACACACGAGATATATFAGATCAACGTAAGGGATGA
    AGTCGCTAGCATGCATGGCATATACGCGATCGATTCGATAGCTAGCG
    
