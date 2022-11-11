<h1>Presentation of the project</h1>

The main objective of this project was to identify the genomic regions accessible by the DNA during the transcription. In order to do this, we re-analyzed the ATAC-seq results from a publication of 2019 ("STATegra, a comprehensive multi-omics dataset of B-cell differentiation in mouse" David Gomez-Cabrero et al. 2019 https://doi.org/10.1038/s41597-019-0202-7). In this publication, an analysis was performed on a B3 murine cellular line. This cell line from the mouse model the pre-B1 stage. After the nuclear translocation of the transcription factor Ikaros, those cells grow to the pre-BII stage. During this stage, the B cells progenitor are subject to a growth arrest and a differentiation.
This B3 cell line was transduced by a retroviral pathway with a vector coding for a fusion protein, Ikaros-REt2, which can control nuclear levels of Ikaros after exposition to the Tamoxifen drug.
After this treatment, the cultures were collected at t=0h and t=24h.

<h2>Experimental design</h2>

About 50 000 cells were collected for each sample. 
There are 3 biological replicates by sample : R1, R2 and R3
Each of the biological replicates was performed for the two cellular stages : 0h and 24h
In total, 6 samples were studied (3 replicates for t=0h and 3 replicates for t=24h)

Each of these samples were sequenced by an Illumina sequencing with Nextera-based sequencing primers. Considering that the sequencing was performed in paired-end, each of the 6 samples has a forward result file and a reverse result file. So, in total, 12 samples were collected for the analysis.

<h3>Raw dataset</h3>

SRR4785152&nbsp;&nbsp;&nbsp;&nbsp;50k_0h_R1_1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.6G&nbsp;&nbsp;&nbsp;&nbsp;50k_0h_R1_2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.6G<br>
SRR4785153&nbsp;&nbsp;&nbsp;&nbsp;50k_0h_R2_1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.5G&nbsp;&nbsp;&nbsp;&nbsp;50k_0h_R2_2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.6G<br>
SRR4785154&nbsp;&nbsp;&nbsp;&nbsp;50k_0h_R3_1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.6G&nbsp;&nbsp;&nbsp;&nbsp;50k_0h_R3_2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.6G<br>

SRR4785341&nbsp;&nbsp;&nbsp;&nbsp;50k_24h_R1_1&nbsp;&nbsp;&nbsp;&nbsp;0.5G&nbsp;&nbsp;&nbsp;&nbsp;50k_24h_R1_2&nbsp;&nbsp;&nbsp;&nbsp;0.5G<br>
SRR4785342&nbsp;&nbsp;&nbsp;&nbsp;50k_24h_R2_1&nbsp;&nbsp;&nbsp;&nbsp;0.5G&nbsp;&nbsp;&nbsp;&nbsp;50k_24h_R2_2&nbsp;&nbsp;&nbsp;&nbsp;0.5G<br>
SRR4785343&nbsp;&nbsp;&nbsp;&nbsp;50k_24h_R3_1&nbsp;&nbsp;&nbsp;&nbsp;0.5G&nbsp;&nbsp;&nbsp;&nbsp;50k_24h_R3_2&nbsp;&nbsp;&nbsp;&nbsp;0.5G<br>

<h1>Workflow</h1>
<h2>Quality control of the raw data</h2>

First of all, we need to perform a quality control on the raw data in order to see the global quality of the dataset. In order to do this, we will create an array of 12 elements which contains the sequencing data (forward and rerverse strand). After that, the fastqc function will be used for each of the elements in the array.

This fisrt quality control can be done thanks to the 'atac_qc_init.slurm' script.

<h2>Elimination of the adaptaters</h2>

After the first quality control and before any analysis, we must eliminate the sequencing primers in the sequences in order to not bias the results. So, we use the trimmomatic function on each element of the previous array.

The trimming of the adaptaters can be done with the 'atac_trim.slurm' script.

The adapters used for the sequencing are Nextera-based primers whose the composition is the following : 
>PrefixNX/1
AGATGTGTATAAGAGACAG<br>
>PrefixNX/2
AGATGTGTATAAGAGACAG<br>
>Trans1
TCGTCGGCAGCGTCAGATGTGTATAAGAGACAG<br>
>Trans1_rc
CTGTCTCTTATACACATCTGACGCTGCCGACGA<br>
>Trans2
GTCTCGTGGGCTCGGAGATGTGTATAAGAGACAG<br>
>Trans2_rc
CTGTCTCTTATACACATCTCCGAGCCCACGAGAC<br>

<h2>Quality control following the trimming</h2>

After the trimming step, it is necessary to make a second quality control in order to be sure of the quality of the remaining sequences and compare the quality between these sequences and the sequences before the trimming.

Once again, we will use the fastqc function but on the results from the trimming.
This can be done thanks to the 'atac_qc_post.slurm' script.

<h2>Mapping</h2>

Now that our sequences are trimmed, we must synchronize the forward and the reverse file of each sample. We will do this by mapping our sequences on the indexed reference genome (Mus_musculus_GRCm39). The mapping will be done with the Bowtie2 tool. 
In order to this, two differnts arrays of 6 elements will be created. In one of them, there will be all the forward files, and in the other there will be the reverse files. The bowtie2 tool, will then take files from each array as an input and map it to the reference genome.

This step can be performed with the "atac_bowtie2.slurm" script.

<h2>Elimination of the duplicates</h2>

As a result of the Bowtie2 tool, we get the alignement of the sequences on the reference genome. However, there is some duplicates that can bias the analysis later. That's why we will remove these duplicates thanks to the MarkDuplicates function from the picard module.

This elimination can be done with the 'atac_picards.slurm" script.

<h2>Data exploration</h2>

Now that we have clear results, we can make some statistics on them. These will be done thanks to the Deeptools module. Indeed, this module will permits to know if the samples are correlated (plotCorrelation function), the coverage of each sample on the genome (bamCoverage) or compare the length of each sample (bamPEFragmentSize function).

However, in order to see correlation between the sample, we must combine all the input BAM files into one. This can be done by the 'atac_array.npz.slurm' script.

The remaining analyses can be done with the 'atac_deeptools.slurm" script.

