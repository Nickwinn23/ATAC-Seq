# bf528-individual-project-Nickwinn23

ATAC-seq Methods

The starting data is two replicates, paired end, human data. Quality control of the two replciates is necessary before any data processing. FastQC 0.12.1-0 will be the first step to provide general quality control of the fastq files. The fastq files will then be trimmed with trimmomatic 0.39. Once the data is preprocessed, alignment can take place. 

The files will then be aligned with Bowtie2 2.5.3. A -X 2000 flag will be used to specify the maximum fragments lengths. The files will then be sorted using samtools sort 1.19.2. It will be important to remove any fragments that align with mitochondrial chromosomes. This can be performed with Smatools view 1.19.2. The sorted BAM files can be given as the input, grep can be utilized to remove any mitochondrial DNA, then the BAM files will be resorted. 

After the filtering process, the reads will need to be shifted due to the tagmentation process. This can be performed using Deeptools' 3.5.4 alignmentSieve command. Once the reads are shifted properly, an overall quality control analysis will be done. Visualizing the fragmentation distribution sizes can be done using ATACSeqQC 1.26.0, which will be done in an R script. 

Peak calling will be the next step in the process and this will be done using MACS 3.0.1 default parameters. Bedtools 2.31.1 intersect peaks will be used to overlay the peaks files of each replicate. A blacklist file will be generated to avoid regions that could yield false positive results, which will require the bedtools intersect command again. Homer 4.11 will be used to handle the peak annotation with the annotatePeaks.p1 command. 

Visualization of the results can be done through motif analysis. Homer's findMotifsGenome.p1 will be performed to see if there is a pattern in the motifs found in the open chromatin. Deeptools will be used to generate a graph of the replicate in regards to the TSS and TES sites. 

In terms of delivaerables ATACSeqQC will produce a fragment length distribution plot. After using Samtools view, a table will be generated to provide the alignments before and after neglectign mitochondrial DNA. Deeptools' plotProfile command will provide a signal coverage plot. Homer and Bedtools will generate reproducible peaks. Homer's findMotifsGenome will provide numerous files for motif analysis. An R script will be utilized to create a gene enrichment analysis on the annotated peaks or a computational tool such as GREAT. Finally, an R script will be produced to display the proportions of regions that appear to have accessible chromatin when called as a peak. 

Here are the questions this experiment will answer:

1) Briefly remark on the quality of the sequencing reads and the alignment statistics, make sure to specifically mention the following:
    Are there any concerning aspects of the quality control of your sequencing reads?
    Are there any concerning aspects of the quality control related to alignment?
    Based on all of your quality control, will you exclude any samples from further       analysis?
    
2) After alignment, quickly calculate how many alignments were generated from each sample in total and how many alignments were against the mitochondrial chromosome
        Report the total number of alignments per sample
        Report the number of alignments against the mitochondrial genome
        
3) After performing peak calling analysis, generating a set of reproducible peaks and filtering peaks from blacklisted regions, please answer the following:
        How many peaks are present in each of the replicates?
        How many peaks are present in your set of reproducible peaks? What strategy did you use to determine “reproducible” peaks?
        How many peaks remain after filtering out peaks overlapping blacklisted regions?
        
4) After performing motif analysis and gene enrichment on the peak annotations, please answer the following:
        Briefly discuss the main results of both of these analyses
        What can chromatin accessibility let us infer biologically?