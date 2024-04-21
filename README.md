 # ATACSeq

## Methods

Fastq files of two ATAC-seq samples were downloaded. Quality control were performed on these samples by using 
fastqc version 0.12.1-0, and then the reads were trimmed using trimmomatic version 0.39. Human genome hg38 were downloaded 
off of Gencode website and an index was built off of it using bowtie2 version 2.5.3. 
Trimmed reads were aligned to the human genome index with a maximum fragment length of 2000 using bowtie2 align. These aligned reads were converted to BAM files, sorted, indexed, and any alignments to the mitochondrial chromosome were removed using samtools version 1.19.2. Using bedtools ver 2.31.1, the BAM files were converted to bed format and shifted to account for tagmentation using alignmentSieve from deeptools ver 3.5.4.
QC was performed on these bed files using ATACseqQC in R.
    Peaks will be called on the bed files with default parameters using MACS v3.0.1. Reproducible peaks were obtained with peaks that had 50% of the peaks in common using the 
bedtools intersect. Peaks that lie in blacklisted areas of the genome will be filtered out using bedtools intersect with the blacklisted genome. Filtered peaks were annotated using the Gencode v45 primary peaks_repr_filtered_annotations. Motifs were found using Homer's findMotifsGenome.pl, with default parameters except for a size of 200.
    IP sample matrices were then computed with the hg38 genes using the computeMatrix command on deeptools with 2000 basepairs 
before the TSS and 2000 bp after the TTS, with all other parameters as default. These matrices were plotted using the plotProfile command 
on deeptools. 




## Questions to Address
Briefly remark on the quality of the sequencing reads and the alignment statistics, make sure to specifically mention the following:

Are there any concerning aspects of the quality control of your sequencing reads?
Are there any concerning aspects of the quality control related to alignment?
Based on all of your quality control, will you exclude any samples from further analysis?

After alignment, quickly calculate how many alignments were generated from each sample in total and how many alignments were against the mitochondrial chromosome

Report the total number of alignments per sample
Report the number of alignments against the mitochondrial genome

After performing peak calling analysis, generating a set of reproducible peaks and filtering peaks from blacklisted regions, please answer the following:

How many peaks are present in each of the replicates?
How many peaks are present in your set of reproducible peaks? What strategy did you use to determine “reproducible” peaks?
How many peaks remain after filtering out peaks overlapping blacklisted regions?

After performing motif analysis and gene enrichment on the peak annotations, please answer the following:

Briefly discuss the main results of both of these analyses
What can chromatin accessibility let us infer biologically?


## Deliverables
Produce a fragment length distribution plot for each of the samples

Produce a table of how many alignments for each sample before and after filtering alignments falling on the mitochondrial chromosome

Create a signal coverage plot centered on the TSS (plotProfile) for the nucleosome-free regions (NFR) and the nucleosome-bound regions (NBR)

You may consider fragments (<100bp) to be those from the NFR and the rest as the NBR.
A table containing the number of peaks called in each replicate, and the number of reproducible peaks

A single BED file containing the reproducible peaks you determined from the experiment.

Perform motif finding on your reproducible peaks

Create a single table / figure with the most interesting results
Perform a gene enrichment analysis on the annotated peaks using a well-validated gene enrichment tool

Create a single table / figure with the most interesting results
Produce a figure that displays the proportions of regions that appear to have accessible chromatin called as a peak (Promoter, Intergenic, Intron, Exon, TTS, etc.)
