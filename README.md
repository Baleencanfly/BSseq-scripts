# Bioinformatic Analysis for Bisulfite Sequencing Data

## Introduction
BSseq-scripts contains scripts for bisulfite sequencing data analysis including data quality control, alignment, quantification and visualization.

## Before starting
Users should first install the following software.

1.	Trim Galore (https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/) 
2.	BSMAP (Xi and Li, 2009; https://code.google.com/archive/p/bsmap/)
3.	Picard (https://broadinstitute.github.io/picard/)
4.	Bamtools (Barnett et al., 2011; https://github.com/pezmaster31/bamtools)
5.	bamUtil (https://github.com/statgen/bamUtil)
6.	BS-SNPer (Gao et al., 2015; https://github.com/hellbelly/BS-Snper)
7.	ViewBS (Huang et al., 2018; https://github.com/xie186/ViewBS)

## Get public files for test (if need)
`wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR850/SRR850328/SRR850328_1.fastq.gz`  
`wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR850/SRR850328/SRR850328_2.fastq.gz`  
`wget http://ftp.ensemblgenomes.org/pub/plants/release-45/fasta/zea_mays/dna/Zea_mays.B73_RefGen_v4.dna.toplevel.fa.gz`

The detailed scripts are in Scripts.md and the format of the intermediate file can be viewed in the data folder.
