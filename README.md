# HAMRbox: A user-friendly adaptation of HAMR
![HAMRbox_Workflow_v3](https://github.com/harrlol/hamrbox/assets/87460010/b477e3a5-9946-41c1-b442-7e013d0881ab)

## Overview
- HAMRbox is a bundle of selected tools that capture different parts of the pipeline tailored for the [High Throughput Annotation of Modified Ribonucleotides](https://github.com/GregoryLab/HAMR), abbreviated HAMR, developed by [Paul Ryvkin et al](https://rnajournal.cshlp.org/content/19/12/1684). HAMRbox aims to make the original method more accessible by automating the tedious pre-processing steps, allowing users to analyze RNA-seq data at an experiment scale. 
- HAMRbox is high-throughput and performs RNA-modification analysis at a bioproject scale. HAMRbox performs constitutive trimming of acquired reads using Trim-Galore, and makes use of STAR as the aligning tool which reduces runtime with a rivaling robustness compared to TopHat2 as suggested in the original pipeline.


## Command Line Arguments and Description

| Command | Description |
| :---: | :---: |
| Required |
| -o | \<project directory\> <br> where you want your entire hamr project to be |
| -t | \<SRA accession list.txt\> or \<folder of raw fastq files\> <br> a txt file of all srr accession code to your desired reads or a path containing them |
| -c | \<filenames for each fastq.csv\> <br> a csv file that corresponds each srr code (or name of fastq file) to your desired nomenclature for each read |
| -g | \<reference genome.fa> <br> a fasta file of the genome of the model organism |
| -i | \<reference genome annotation.gff3> <br> a gff3 file of the genome of the model organism, note we require gff3 instead of gtf |
| -l | \<read length\> <br> an integer, the read length of this sequencing experiment, if non-unanimous use the shortest length |
| -s | \<genome size in bp\> <br> an integer, the number of base pairs of the genome of this model organism |
| -e | \<genome annotation generator code\> <br> see below for abbreviation code, one code per organism/cultivar |
| Optional |
| -a | \[use Tophat2 instead of STAR\] <br> default uses STAR |
| -b | \[Tophat2 library choice: fr-unstranded, fr-firststrand, fr-secondstrand\] <br> default=fr-firststrand |
| -f | \[filter\] <br> default=filter_SAM_number_hits.pl |
| -Q | \[HAMR: minimum qualuty score\] <br> default=30 |
| -C | \[HAMR: minimum coverage\] <br> default=50 |
| -E | \[HAMR: sequencing error\] <br> default=0.01 |
| -P | \[HAMR: maximum p-value\] <br> default=1 |
| -F | \[HAMR: maximum FDR\] <br> default=0.05 |
| -m | \[HAMR model\] <br> default=euk_trna_mods.Rdata |
| -n | \[number of threads\] <br> default=4 |
| -h | \[help message\]|

## Annotation Generator Code
| Abbreviation Code | Organism |
| --- | --- |
| AT | Arabidopsis thaliana |
| BD | Brachypodium distachyon |
| ZM | Zea mays |
| OSJ | Oryza sativa japonica |
| OSI | Oryza sativa indica |
| OSIR64 | Oryza sativa IR64 |


## Running HAMRbox (demo)

Pull docker image from this git
```
docker pull harrlol/hamrbox
```

Download genome fastq file for Arabidopsis thaliana
```
wget -qO- https://ftp.ensemblgenomes.ebi.ac.uk/pub/plants/release-57/fasta/arabidopsis_thaliana/dna/Arabidopsis_thaliana.TAIR10.dna.toplevel.fa.gz | tar xvz 
```

Download annotation gff3 file for Arabidopsis thaliana
```
wget -qO- https://ftp.ensemblgenomes.ebi.ac.uk/pub/plants/release-57/gff3/arabidopsis_thaliana/Arabidopsis_thaliana.TAIR10.57.gff3.gz | tar xvz 
```

Run HAMRbox
```
docker run \
  --rm \
  -v $(pwd):/working-dir \
  -o /working-dir \
  harrlol/hamrbox \
  -t ~/demo/PRJNA596803_list.txt \
  -c ~/demo/PRJNA596803_filenames.csv \
  -g ~/path/to/genome.fasta \
  -i ~/path/to/genomeannotation.gff3 \
  -l 50 \
  -s 135000000 \
  -e AT
```
