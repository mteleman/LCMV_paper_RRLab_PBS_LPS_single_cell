# LCMV Paper codes and datafiles repository

## Article information

**Title:** Post-natal meningeal macrophages protect against viral neuroinfection.

**Authors:** Julie Rebejac(1), Elisa Eme-Scolan(1), Matei Teleman(1), Lionel Spinelli(1), Emeline Gallo(1), Annie Roussel-Queval(1), Ana Zarubica(2), Amandine Sansoni(2), Quentin Bardin(2), Philippe Hoest(3), Bernard Malissen(1,2), Marie-Cécile Michallet(4), Toby Lawrence(1,5), Monica Manglani(6), Dorian B. McGavern(6) & Rejane Rua(1)

(1) Aix Marseille University, Inserm, CNRS, Immunology Center of Marseille-Luminy, Marseille, France

(2) Centre d’Immunophénomique, Aix Marseille Université, INSERM, CNRS, 13288 Marseille, France
(3) TERI (Tumor Escape, Resistance and Immunity) Department, Centre de Recherche en Cancérologie de Lyon, Centre Léon Bérard, Université de Lyon, Université Claude Bernard Lyon 1, INSERM 1052, CNRS 5286, 69008 Lyon, France
(4) Centre for Inflammation Biology and Cancer Immunology, Cancer Research UK King's Health Partners Centre, School of Immunology and Microbial Sciences, King's College London, London SE1 1UL, UK.
(5) Viral Immunology and Intravital Imaging Section, National Institute of Neurological Disorders and Stroke, National Institutes of Health, Bethesda, MD 20892, USA


% Corresponding author: E-mail: rua@ciml.univ-mrs.fr

**Summary:**
Due to the vital importance of the Central Nervous System (CNS), its potential infection and inflammation have to be tightly controlled. The surface of the CNS is connected to the periphery by a rich and complex tissue, the meninges. They contain a vast network of macrophages subdivided in at least two subpopulations endowed with elusive functions: a neonatal, MHC-II negative macrophage population, and an post-natal population expressing MHC-II. Using in situ-histocytometry, flow cytometry, and single-cell RNA sequencing approaches, we showed that those populations have opposite dynamic behaviors in response to in vivo peripheral challenges such as LPS, SARS-CoV2 and lymphocytic choriomeningitis virus (LCMV), with an apparent contraction of the MHC-II+ population. Focusing on LCMV infection in experimental mouse models and using innovative pharmacological and genetic depletion strategies, we show that meningeal macrophages (MM) represent an early line of protection against this neuroinvasive pathogen. In their absence, specific areas in the meninges became highly infected, leading to fatal brain disease. While their intrinsic sensing of viral replication through the Mitochondrial antiviral-signaling protein (MAVS) was dispensable, sensing of IFNs through the STAT1 pathway played an important role in controlling viral spread. Unexpectedly, the post-natal MHC-II+ macrophage population had an important role in controlling neuroinfection, by shutting down biosynthesis pathways and efficiently blocking viral replication. This work helps understanding the spatial organization of the brain defense system and the cellular and molecular mechanisms involved in CNS protection.

DOI : [10.1016/j.celrep.2020.108004](https://doi.org/10.1016/j.celrep.2020.108004) 

---
---

## Goal of the github
This github project contains the instructions and material to reproduce the analysis reported in the article (and more).
Source code (scripts and dockerfiles) are available in the github repository. Required data and builded Docker/Singularity images are available on download. Instructions to reproduce the analysis are provided below.

To reproduce the analysis, you have to first, prepare the environments (see "Prepare the Environments" section below), then execute the analysis step by step (see "Run the analysis" section below).

---
---

## Description of the datasets

As described in the article, there is 5 datasets in this study. One datset is a bulk sequencing of mRNA on two embryo tissues (Fetal Liver and Periphery) at stage 13.5 days. The other 4 datasets are single-cell sequencing of mRNA on two embryo tissues (Fetal Liver and Periphery) and two stages (13.5 and 14.5 days). When downloading the code and data, you will obtains 5 sub-folders with names as below:

    BecomingLTi
    ├── Embryo_Bulk_Stage13.5_2tissues : Bulk RNA-seq of Embryo Fetal Liver and periphery tissues at stage 13.5 days
    ├── Embryo_Stage13.5_FetalLiver : Single-cell RNA-seq of Embryo Fetal Liver tissue at stage 13.5 days
    ├── Embryo_Stage13.5_Periphery_CellRangerV3 : Single-cell RNA-seq of Embryo Periphery tissue at stage 13.5 days
    ├── Embryo_Stage14.5_FetalLiver :  : Single-cell RNA-seq of Embryo Fetal Liver tissue at stage 14.5 days
    └── Embryo_Stage14.5_Periphery_CellRangerV3 : Single-cell RNA-seq of Embryo Periphery tissue at stage 14.5 days

---
---

## Prepare the environments

In order to prepare the environment for analysis execution, it is required to:

- Clone the github repository and set the WORKING_DIR environment variable
- Download the docker image tar file and the singularity img files
- Install Docker and Singularity
- Load the docker image on your system
- Download the pre-processed data (Count table for bulk RNA-seq and CellRanger results for single-cell RNA-seq)

Below you will find detailed instruction for each of these steps.

### Clone the github repository

Use you favorite method to clone this repository in a chosen folder. This will create a folder "BecomingLTi" with all the source code. 

Then, you must set an environment variable called WORKING_DIR with a value set to the path to this folder.

For instance, if you have chosen to clone the Git repository in "/home/spinellil/workspace", then the WORKING_DIR variable will be set to "/home/spinellil/workspace/BecomingLTi"

**On linux:**

    export WORKING_DIR=/home/spinellil/workspace/BecomingLTi

### Download the raw data

Each sample needs its own "00_RawData" sub-folder containing the initial data used by the analysis. Those data can be downloaded from Zenodo and uncompressed. The Zenodo dataset DOI are [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3946361.svg)](https://doi.org/10.5281/zenodo.3946361), [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3947819.svg)](https://doi.org/10.5281/zenodo.3947819) and [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3946154.svg)](https://doi.org/10.5281/zenodo.3946154).

To download and uncompress the data, use the following code:

**On linux:**

    cd $WORKING_DIR
    wget https://zenodo.org/record/3946154/files/SPlab_BecomingLTi_Bulk_Stage13.5_2tissues_00_RawData.tar.gz?download=1 -O SPlab_BecomingLTi_Bulk_Stage13.5_2tissues_00_RawData.tar.gz
    tar zxvf SPlab_BecomingLTi_Bulk_Stage13.5_2tissues_00_RawData.tar.gz
    
    wget https://zenodo.org/record/3946361/files/SPlab_BecomingLTi_Stage13.5_FetalLiver_00_RawData.tar.gz?download=1 -O SPlab_BecomingLTi_Stage13.5_FetalLiver_00_RawData.tar.gz
    tar zxvf SPlab_BecomingLTi_Stage13.5_FetalLiver_00_RawData.tar.gz
    
    wget https://zenodo.org/record/3946154/files/SPlab_BecomingLTi_Stage13.5_Periphery_CellRangerV3_00_RawData.tar.gz?download=1 -O SPlab_BecomingLTi_Stage13.5_Periphery_CellRangerV3_00_RawData.tar.gz
    tar zxvf SPlab_BecomingLTi_Stage13.5_Periphery_CellRangerV3_00_RawData.tar.gz
    
    wget https://zenodo.org/record/3947819/files/SPlab_BecomingLTi_Stage14.5_FetalLiver_00_RawData.tar.gz?download=1 -O SPlab_BecomingLTi_Stage14.5_FetalLiver_00_RawData.tar.gz
    tar zxvf SPlab_BecomingLTi_Stage14.5_FetalLiver_00_RawData.tar.gz
    
    wget https://zenodo.org/record/3946154/files/SPlab_BecomingLTi_Stage14.5_Periphery_CellRangerV3_00_RawData.tar.gz?download=1 -O SPlab_BecomingLTi_Stage14.5_Periphery_CellRangerV3_00_RawData.tar.gz
    tar zxvf SPlab_BecomingLTi_Stage14.5_Periphery_CellRangerV3_00_RawData.tar.gz

Once done, you may obtain the following subfolder structure, each of them containing several files.

    BecomingLTi
    ├── Embryo_Bulk_Stage13.5_2tissues
    │   └── 00_RawData
    ├── Embryo_Stage13.5_FetalLiver
    │   └── 00_RawData
    ├── Embryo_Stage13.5_Periphery_CellRangerv3
    │   └── 00_RawData
    ├── Embryo_Stage14.5_FetalLiver
    │   └── 00_RawData
    └── Embryo_Stage14.5_Periphery_CellRangerv3
        └── 00_RawData

### Download the reference files

The study uses references (genome annotations) you have to download. The annotations used during the study are available on Zenodo [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3949849.svg)](https://doi.org/10.5281/zenodo.3949849). Use the following command to download the tarball file and uncompress it.

Note: Since the reference files are used for the 4 single-cell samples analysis, they must be present in all the sample folder in the same 01_Reference subfolder. Instead of copying the files, we will create symbolic links:

**On linux:**

    cd $WORKING_DIR
    wget https://zenodo.org/record/3949849/files/SPlab_BecomingLTi_01_Reference.tar.gz?download=1 -O SPlab_BecomingLTi_01_Reference.tar.gz
    tar zxvf SPlab_BecomingLTi_01_Reference.tar.gz
    ln -s Embryo_Stage13.5_FetalLiver/01_Reference Embryo_Stage13.5_Periphery_CellRangerV3/01_Reference
    ln -s Embryo_Stage13.5_FetalLiver/01_Reference Embryo_Stage14.5_FetalLiver/01_Reference
    ln -s Embryo_Stage13.5_FetalLiver/01_Reference Embryo_Stage14.5_Periphery_CellRangerV3/01_Reference

These commands will create 4 sub-folders named 01_Reference:

    BecomingLTi
    ├── Embryo_Stage13.5_FetalLiver
    │   └── 01_Reference
    ├── Embryo_Stage13.5_Periphery_CellRangerv3
    │   └── 01_Reference
    ├── Embryo_Stage14.5_FetalLiver
    │   └── 01_Reference
    └── Embryo_Stage14.5_Periphery_CellRangerv3
        └── 01_Reference

### Download the Docker and Singularity images

Docker image tar file and Singularity img files are stored on Zenodo [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3949849.svg)](https://doi.org/10.5281/zenodo.3949849). Open a shell command and change dir to the root of the cloned Git repository (WORKING_DIR). Then execute the following commands to download the tarball file and untar  it:

**On linux:**

    cd $WORKING_DIR
    wget https://zenodo.org/record/3949849/files/SPlab_BecomingLTi_02_containers.tar.gz?download=1 -O SPlab_BecomingLTi_02_containers.tar.gz
    tar zxvf SPlab_BecomingLTi_02_containers.tar.gz

These commands will create 2 sub-folders named 02_Container:

    BecomingLTi
    ├── Embryo_Bulk_Stage13.5_2tissues
    │   └── 02_Container
    └── Embryo_Stage13.5_FetalLiver
        └── 02_Container

The first one contains a Docker image tar file used for the bulk RNA-seq analysis. The second one contains the Singularity images for the single-cell RNA-seq analysis. Since the singularity images are used for the 4 single-cell samples analysis, they must be present in all the sample folder in the same 02_Container subfolder. Instead of copying the image files, we will create symbolic links:

**On linux:**

    cd $WORKING_DIR
    ln -s Embryo_Stage13.5_FetalLiver/02_Container Embryo_Stage13.5_Periphery_CellRangerV3/02_Container
    ln -s Embryo_Stage13.5_FetalLiver/02_Container Embryo_Stage14.5_FetalLiver/02_Container
    ln -s Embryo_Stage13.5_FetalLiver/02_Container Embryo_Stage14.5_Periphery_CellRangerV3/02_Container

### Install Docker and Singularity

You need to install Docker and Singularity v2.6 on your system.

- To install Docker, follow the instructions here : https://docs.docker.com/get-docker/

- To install Singularity v2.6, follow the instructions here : https://sylabs.io/guides/2.6/admin-guide/

### Load docker images on the system

In order to execute analysis of the bulk RNA-seq, you must load the provided docker image onto your Docker. Docker must be installed on your system. 
See https://docs.docker.com/install/ for details on Docker installation.
Open a shell command and type:

**On linux:**

    docker load -i $WORKING_DIR/Embryo_Bulk_Stage13.5_2tissues/02_Container/splab_ilcyou_deg_gsea.tar

This command may take some time. If you encounter an issue loading some docker image layer, try again. Sometimes issue would be resolved. 

### Install Snakemake

If you want to take advantage of the workflow management we used for the single-cell RNA-seq analysis, you have to install Snakemake. See the official instruction and use your prefered solution:

https://snakemake.readthedocs.io/en/stable/getting_started/installation.html

---
---

## Run the analysis

There are two types of analysis in this study : bulk RNA-seq and single-cell RNA-seq. The bulk RNA-seq analysis uses the Docker image you loaded. The single-cell RNA-seq analysis uses the Singularity images and optionnaly Snakemake.

### Run the bulk RNA-seq analysis

The RNA-seq analysis are in two steps (step1 and step2). The first step make the QC, study the differentially expressed genes and their functionnal enrichment. The second step study the pattern of evolution of group of genes along the cell types (see article methods).

To run the step1 analysis, use the following command:

**On Linux:**

    docker run -v $WORKING_DIR:$WORKING_DIR -e WORKING_DIR=$WORKING_DIR splab_ilcyou_deg_gsea 'cd $WORKING_DIR/Embryo_Bulk_Stage13.5_2tissues/03_Script/step1;Rscript launch_reports_compilation.R'

To run the step2 analysis, use the following command:

**On Linux:**

     docker run -v $WORKING_DIR:$WORKING_DIR -e WORKING_DIR=$WORKING_DIR splab_ilcyou_deg_gsea 'cd $WORKING_DIR/Embryo_Bulk_Stage13.5_2tissues/03_Script/step2;Rscript launch_reports_compilation.R'

Each analysis will generate a result in $WORKING_DIR/Embryo_Bulk_Stage13.5_2tissues/05_output/step1 or $WORKING_DIR/Embryo_Bulk_Stage13.5_2tissues/05_output/step2.
In the output of the analysis, you will find a HTML file that contains the report of the analysis, with all figures. Some extra file are generated to export data in plain text.


### Run the single-cell RNA-seq analysis

The study contains 4 samples of single-cell RNA-seq data. Each sample have 5 step of analysis you will find the R script files in the subfolder 03_Script. The 5 steps are:

 * 01_QC : General quality control and bad cell removal
 * 02_GlobalHeterogeneity : First study of cell heterogeneity and sample contamination by undesired cell types
 * 03_GlobalHeterogeneity_NoContamination : Study of cell heterogeniety in absence of contamination
 * 04_Dynamics_Monocle : analysis of the cellular process dynamics using pseudotime analysis by Monocle
 * 05_Dynamics_RNAVelocity : analysis of the cellular process dynamics using RNA velocity (Velocyto)

Each step of analysis generates its own HTML report file and several output files. Some output files of some steps are used by other steps, making a complete workflow of analysis.

The simpliest way to run the complete single-cell analysis of a sample is to use the Snakemake workflow dedicated to each sample. The workflow is controled by a snakefile stored in the 04_Workflow subfolder of each sample folder. This workflow uses Singularity images (see above) to control the software environment for each analysis step. So you need both Snakemake and Singularity installed on your system to use this workflow.

In order to use the snakemake workflow, please type first the following commands:

     cd $WORKING_DIR
     ln -s Embryo_Stage13.5_FetalLiver/04_Workflow/snakefile.yml Embryo_Stage13.5_FetalLiver/snakefile.yml
     ln -s Embryo_Stage13.5_Periphery_CellRangerV3/04_Workflow/snakefile.yml Embryo_Stage13.5_Periphery_CellRangerV3/snakefile.yml
     ln -s Embryo_Stage14.5_FetalLiver/04_Workflow/snakefile.yml Embryo_Stage14.5_FetalLiver/snakefile.yml
     ln -s Embryo_Stage14.5_Periphery_CellRangerV3/04_Workflow/snakefile.yml Embryo_Stage14.5_Periphery_CellRangerV3/snakefile.yml

To run the analysis for the Embryo_Stage13.5_FetalLiver (for instance), then run the following commands:

Note: you have to manually change the "$WORKING_DIR" string in the snakemake command below by the value of the environment variable (i.e the path where you clone the project) because snakemake may not interpret the variable name correctly:

     cd $WORKING_DIR/Embryo_Stage13.5_FetalLiver
     snakemake -r --snakefile snakefile.yml --use-singularity --singularity-args "-B $WORKING_DIR:$WORKING_DIR"
     
To execute the analysis of the other sample, simply change folder to the target sample and run again the same snakemake command.
