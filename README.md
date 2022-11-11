<h1><center>Presentation of the project</center></h1>

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
