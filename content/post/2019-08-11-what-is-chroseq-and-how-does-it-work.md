---
title: What is ChROseq and how does it work
author: Sichong Peng
date: '2019-08-11'
slug: what-is-chroseq-and-how-does-it-work
categories:
  - Genetics
tags:
  - Sequencing
  - bioinformatics
image:
  caption: ''
  focal_point: ''
---

At the moment of writing this post, I'm sitting on the plane flying to Cornell. There I will learn a beautiful technique called Chromatin Run-On and Sequencing, or ChRO-seq.

Thirteen hours of travel is getting to the point of breaking my soul -- I have finished most of work I can comfortablely do with one screen on a samll laptop. So I decided to write down what I know so far about ChRO-seq in preparation for my upcoming training tomorrow. I will keep updating this post as I learn more about this technique.

## What is ChROseq

ChRO-seq is a variant of Run-On sequencing developed by Danko lab at Cornell (Chu et. al., 2018). In essence, it profiles nascent RNA by capturing RNA polII and DNA interaction. Below is a diagram from the authors depicting the major steps of a ChRO-seq experiment:

![Summary of ChROseq methods](/img/ChROseq.png)

As shown above, insoluble chromatin is first isolated from tissues or cell culture. Isolated chromatin then gets re-suspended through sonication. Run-on reaction is done by incubating RNA polII and DNA complex with biotinylated rNTP. A complementary biotinylated NTP gets added on to the attached nascent RNA and prevents any further elongation.  

Once run-on reaction is completed, 3 rounds of streptavidin bead purification are performed to purify extended nascent RNA, add 3' adapter, remove 5'cap and add 5' adapter. After adapters are added to both ends, a cDNA library is constructed from the nascent RNAs and a single end illumina sequencing is performed from 3'end.

## What does ChRO-seq tell me
Like any run-on sequencing techique, ChRO-seq precisely captures nascent RNA when compared to general RNAseq. This means that:

1. ChRO-seq gives a more accurate quantification of DNA transcription, as opposed to RNAseq, which describes a result of DNA transcription and RNA degradation.
2. The fact that ChROseq is not noised by RNA degradation also means that it is able to capture many non-coding RNAs that have a short life span in cells and thus difficult for RNAseq to capture.
3. ChRO-seq provides a snap shot of transcription activity. As revealed by other run-on sequencing, it can identify RNA polII pausing sites.
4. Like other run-on sequencing, ChRO-seq can also be used to identify different types of transcriptions, as observed by Core et. al., 2008.

## What does ChRO-seq not tell me
Because ChRO-seq captures nascent RNA, naturally, it does not contain any post-transcriptional level information like splicing, polyadenylation, and other RNA or protein modifications.

## How does ChRO-seq compare to other RNA-related techniques?
||RNAseq|ChRO-seq|PRO-seq|GRO-seq
|---|---|---|---|---|
|RNA captured|mature RNA|Nascent RNA|Nascent RNA|Nascent RNA|
|Quantify transcription|Yes(with degradation)|Yes|Yes|Yes|
|Single base resolution|Yes|Yes|Yes|No|
|Material type|RNA|Insoluble chromatin|Nuclei|Nuclei|
