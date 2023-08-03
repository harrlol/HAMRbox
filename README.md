# HAMRbox: A User-friendly adaptation of HAMR

## Overview
- HAMRbox is a box of selected tools that capture different parts of the pipeline tailored for the [High Throughput Annotation of Modified Ribonucleotides](https://github.com/GregoryLab/HAMR), abbreviated HAMR, developed by [Paul Ryvkin et al](https://rnajournal.cshlp.org/content/19/12/1684). HAMRbox aims to make the original method more accessible by automating the tedious pre-processing steps, allowing users to analyze RNA-seq data at an experiment scale. 
- HAMRbox is high-throughput and performs RNA-modification analysis at a bioproject scale. HAMRbox performs constitutive trimming of acquired reads using Trim-Galore, and makes use of STAR as the aligning tool which reduces runtime with a comparable robustness compared to TopHat2 as suggested in the original pipeline.


## Command Line Arguments and Description
