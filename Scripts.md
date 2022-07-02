## Perform quality control analysis for sequencing data
`trim_galore --phred33 --fastqc --fastqc_args "--noextract --outdir /path/to/rawdata/fastqc/" -o /path/to/rawdata/trimgalore/ --paired /path/to/rawdata/fastq/SampleX_R1.fq.gz /path/to/rawdata/fastq/SampleX_R2.fq.gz`

## Align reads to reference genome
`bsmap -a /path/to/rawdata/trimgalore/SampleX_R1_val_1.fq.gz -b /path/to/rawdata/trimgalore/SampleX_R2_val_2.fq.gz -d /path/to/REFfile/REFfile.fa -o /path/to/aligntoREF/BAM/SampleX.bam -v 5 -r 0 -p 8 -q 20 -A AGATCGGAAGAGCGGTTCAGCAGGAATGCCG`(adapter sequence according to each sample)

## Remove PCR duplicates
`java -jar picard.jar SortSam -I /path/to/aligntoREF/BAM/SampleX.bam -O /path/to/aligntoREF/BAM/SampleX_sorted.bam -SORT_ORDER coordinate`

`java -jar picard.jar MarkDuplicates -I /path/to/aligntoREF/BAM/SampleX_sorted.bam -O /path/to/aligntoREF/BAM/SampleX_sorted_MarkDup.bam -M /path/to/aligntoREF/DuplicateRate/SampleX_MarkDup.txt --REMOVE_DUPLICATES true`

## Keep properly mapped pairs
`bamtools filter -isMapped true -isPaired true -isProperPair true -in /path/to/aligntoREF/BAM/SampleX_sorted_MarkDup.bam -out /path/to/aligntoREF/BAM/SampleX_sorted_MarkDup_paired.bam`

## Clip overlapping read pairs
`bamUtil/bin/bam clipOverlap --in /path/to/aligntoREF/BAM/SampleX_sorted_MarkDup_paired.bam --out /path/to/aligntoREF/BAM/SampleX_sorted_MarkDup_paired_clipOverlap.bam --stats`

## Calculate DNA methylation levels in each Cytosines
`/bsmap-2.90/methratio.py -o /path/to/aligntoREF/BSMAPratio/SampleX -d /path/to/REFfile/REFfile.fa -u -z -r /path/to/aligntoREF/BAM/SampleX_sorted_MarkDup_paired_clipOverlap.bam`

## Calculate the conversion efficiency of unmethylated cytosine
`awk -F "\t" '{if($1=="Pt") print}' /path/to/aligntoREF/BSMAPratio/SampleX | awk '{sum1 += $7; sum2 +=$8}END{print sum1"\t"sum2"\t"100-sum1/sum2\*100}' > /path/to/aligntoREF/ConversionRate/SampleX_conversion_rate.txt`
