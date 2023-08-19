# HAMRbox: A user-friendly adaptation of HAMR
![HAMRbox_Workflow_v3](https://github.com/harrlol/hamrbox/assets/87460010/65f3e8c2-634f-433c-a3d8-777ac64c71f1)
## Overview
- HAMRbox is a bundle of selected tools that capture different parts of the pipeline tailored for the [High Throughput Annotation of Modified Ribonucleotides](https://github.com/GregoryLab/HAMR), abbreviated HAMR, developed by [Paul Ryvkin et al](https://rnajournal.cshlp.org/content/19/12/1684). HAMRbox aims to make the original method more accessible by automating the tedious pre-processing steps, allowing users to analyze RNA-seq data at an experiment scale. 
- HAMRbox is high-throughput and performs RNA-modification analysis at a bioproject scale. HAMRbox performs constitutive trimming of acquired reads using Trim-Galore, and makes use of STAR as the aligning tool which reduces runtime with a rivaling robustness compared to TopHat2 as suggested in the original pipeline.


## Command Line Arguments and Description

| Command | Description |
| --- | --- |
| Required |
| -o | \<project directory\> |
| -t | \<SRA accession list.txt or folder of raw fastq files\> |
| -c | \<filenames for each fastq.csv\>|
| -g | \<reference genome.fa> |
| -i | \<reference genome annotation.gff3> |
| -l | \<read length\> |
| -s | \<genome size in bp \> |
| Optional |
| -a | \[use TopHat2 instead of STAR\]|
| -b | \[Tophat library choice: fr-unstranded, fr-firststrand, fr-secondstrand\]|
| -f | \[filter\]|
| -e | \[genome annotation generator\]|
| -Q | \[HAMR: minimum qualuty score, default=30\]|
| -C | \[HAMR: minimum coveragem default=50\]|
| -E | \[HAMR: sequencing error, default=0.01\]|
| -P | \[HAMR: maximum p-value, default=1\]|
| -F | \[HAMR: maximum fdr, default=0.05\]|
| -m | \[HAMR model\]|
| -n | \[number of threads, default=4\]|
| -h | \[help message\]|


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
docker run --rm -v $(pwd):/working-dir -o /working-dir harrlol/hamrbox -t ~/demo/PRJNA596803_list.txt -c ~/demo/PRJNA596803_filenames.csv -g ~/path/to/genomefiles -l 50 -s 135000000
```
