# hemat_bairdii_transcriptome
 
First project upon starting grad school - examining differential expression of shared hematodinium/C. bairdii libraries at various temperatures and at different time points.

Data has same libraries and same general notation as Grace Crandall's research

Date started project: 2020/10/25 (approximation)
Date started Github repo: 2020/12/11

Contact: Aidan Coyle, afcoyle@uw.edu
Roberts Lab, UW-SAFS

**Process and Workflow**
My workflow begins with downloading trimmed libraries of _Hematodinium_-infected Tanner crab (_Chionoecetes bairdi_), along with a transcriptome containing both _Hematodinium_ and _C. bairdi_ genes that is unfiltered by taxonomy. The transcriptome is used to create an index using [kallisto](https://pachterlab.github.io/kallisto/manual), and our trimmed libraries are then quantified via pseudoalignment to our index.

From the quantified kallisto output, I use [this script from the Trinity pipeline](https://github.com/trinityrnaseq/trinityrnaseq/wiki/Trinity-Transcript-Quantification) to create a matrix of counts. That matrix of counts is then fed into [DESeq2](https://bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html), which produces tables of differentially-expressed genes and of all genes, both with the corresponding p-values and adjusted p-values. 

I then take the table of transcript IDs for all genes and cross-reference it with [the BLASTx annotation of the transcriptome we downloaded earlier](https://gannet.fish.washington.edu/Atumefaciens/20200508_cbai_diamond_blastx_transcriptome-v2.0/20200507.C_bairdi.Trinity.blastx.outfmt6) to produce a table of all accession IDs. That table is then cross-referenced with the Swiss-Prot database to produce a tab-delimited two-column table of gene IDs and GO terms.

I also take the DESeq output table of all genes and cross-reference it again with the BLASTx annotation to produce a CSV table of gene IDs and unadjusted p-values. 

The tab-delimited two-column table and the two-column CSV are then used as input for [GO-MWU](https://github.com/z0on/GO_MWU), which performs a gene ontology analysis and determines which pathways are significantly enriched based on GO annotations.

**Data Sources**

*Libraries*


[Trimmed individual libraries downloaded from here](https://gannet.fish.washington.edu/Atumefaciens/20200318_cbai_RNAseq_fastp_trimming/) at 22:00 PST on 2021-02-02

[Pooled libraries downloaded from here](https://gannet.fish.washington.edu/Atumefaciens/20200414_cbai_RNAseq_fastp_trimming/) at 24:00 PST on 2021-02-02

Mapping between libraries and treatments is available [at this Google doc](https://docs.google.com/spreadsheets/d/1d17yg5F5gKKC66O8QkTIlPxljJeuX7ZsG46pkBr1lNQ/edit#gid=0)

*Transcriptome*

[Transcriptomes downloaded from here](https://owl.fish.washington.edu/halfshell/genomic-databank/). at 01:00 PST on 2021-02-03

Transcriptome checksums, along with additional information (including BLASTx annotation, GO terms annotation, etc) [available here](https://github.com/RobertsLab/resources/wiki/Genomic-Resources)

*Swiss-Prot Database*

[Swiss-Prot database manually downloaded from here](https://www.uniprot.org/uniprot/?) at 15:00 on 2021-02-09.
Downloaded an uncompressed .tab file that includes all GO terms

**Tool Information**

R: 
```
platform       x86_64-w64-mingw32          
arch           x86_64                      
os             mingw32                     
system         x86_64, mingw32             
status                                     
major          4                           
minor          0.3                         
year           2020                        
month          10                          
day            10                          
svn rev        79318                       
language       R                           
version.string R version 4.0.3 (2020-10-10)
nickname       Bunny-Wunnies Freak Out    
```

kallisto: version 0.46.0

Trinotate: version 3.2.1

Operating system:
```
Windows 10, x64 (OS build: 18363.1256)
Running WSL version 1
```

R packages:
```
apeglm: 1.12.0
BiocManager: 1.30.10
DESeq2: 1.30.0
tidyverse: 1.3.0
topGO: 2.42.0
VennDiagram: 1.6.20
vsn: 3.58.0
```

**Completed Analysis**

Following scripts 01 through 06, I completed analysis with GO-MWU following the pipeline described at the top of this file. 

**Plan for the Future**

In weeks 6-10, I plan to reorient towards a weighted correlation network analysis to examine the effects of both time and temperature treatment. Furthermore, I hope to differentiate _Hematodinium_ DEGs from _C. bairdi_ DEGs, and look at which _Hematodinium_ genes are impacted by temperature on an individual basis.