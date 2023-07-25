# Analysis of Medicago-AMF single-nuclei and spatial transcriptomics datasets


This is a repository for the publication "Spatial co-transcriptomics of the arbuscular mycorrhizal symbiosis" in which authors applied single-nuclei RNA-seq and spatial RNA-seq to the symbiosis between Medicago truncatula and Rhizophagus irregularis.

***

### All figures can be produced using code found in the following Juptyer Notebooks:

1. sNucRNAseq_med_AMF.ipynb: Figure 1a, Figure 3a, Figure 3b, Figure 4b, Figure 4c, Supp. Sheet 4  
2. sNucRNAseq_med_all.ipynb: Supp Figure 3  
3. spatialRNAseq_pre_integration.ipynb: spatial data conversion into seurat object + filtering/normalization
4. spatialRNAseq_integration.ipynb: spatial object integration, Supp Figure 4
5. spatialRNAseq_post_integration.ipynb: Figure 2b, Figure 2c, Figure 4a (data), Figure 4b, Figure 5c
6. colonizationanalysis.ipynb: Supp Figure 2   

Fastq files, Cellranger and Spaceranger matrix files, and fully processed .RDS Seurat Object files can be download here: [INSERT LINK HERE].

The following packages are required:  
(maybe this can be removed since we have the bcoli docker image info below?)  
  
"Seurat"
"ggplot2"
"patchwork"
"dplyr"
"here"
"tidyverse"
"viridis"
"lattice"
"reshape2"
"cowplot"
"Matrix"
"Matrix.utils"
"edgeR"
"S4Vectors"
"SingleCellExperiment"
"pheatmap"
"apeglm"
"png"
"DESeq2"
"RColorBrewer"
"data.table"

***

For optimal reproducibility, it is best to use the docker image listed below rather than rely on packages downloaded locally. You may also find it necessary to use NERSC or a cloud computing platform to analyze larger datasets; below are instructions for pulling the docker image during an interactive R session on NERSC or in a NERSC-hosted Jupyter notebook (preferred but a few more steps to set up). 

***

## Very basic instructions for pulling a docker image that supports these Jupyter Notebooks:

1. docker is installed on your computer and running (might as well be the latest version)
2. adjust docker preferences>resources to at least 8GB memory and at least 16GB disk image size
3. in terminal:
  
> docker pull bcoli/renv_single_cell:2.1.1

> docker run --rm --mount type=bind,source="your-project-directory",target="/home/rstudio/" -p 8787:8787 bcoli/renv_single_cell:2.1.1

4. in web browser, type: http://localhost:8787

Username: rstudio

PW: provided in terminal 


## To use this docker image for R on NERSC (for larger objects)

1. be in an interactive node
2. be in directory where files are

run:

> shifterimg pull bcoli/renv_single_cell:2.0.1
> shifter --image bcoli/renv_single_cell:2.0.1 
> R




## To use R in a Jupyter notebook on NERSC

To create a kernel to use shifter to connect to the bcoli/renv_single_cell:2.1.1 docker image:

Log in to Perlmutter and navigate to:
~/.local/share/jupyter/kernels

> mkdir seurat-shifter
> cd seurat-shifter

> vim kernel.json

this kernel.json should contain the following:


> {  "argv": ["shifter","--image=bcoli/renv_single_cell:2.1.1","R","--slave", "-e", "IRkernel::main()", "--args", "{connection_file}"],       
>   "display_name": "seurat_shifter",  "language": "R"
> }

Go to 'jupyter.nersc.gov' and select a CPU (shared or exclusive) on Perlmutter– this kernel should now be available

### R objects identities: 
see [doc](https://docs.google.com/spreadsheets/d/1qOwmLMpmt2HH15gKPDxhaYfOm3qaqwchRPpiCUTjFzI/edit#gid=413368883](https://docs.google.com/spreadsheets/d/1qOwmLMpmt2HH15gKPDxhaYfOm3qaqwchRPpiCUTjFzI/edit?usp=sharing)

### reference genomes:
Medicago truncatula genome assembly and annotation: MedtrA17_4.0

Rhizophagus irregularis genome assembly and annotation: Rir_HGAP_ii_V2 (DAOM 181602, DAOM 197198)
.

Please reach out to Karen Serrano at karenserrano@lbl.gov or Margot Bezrutcyzk at mbezrutczyk@lbl.gov for any questions.



