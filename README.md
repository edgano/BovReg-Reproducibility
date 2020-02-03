# BovReg Reproducibility

This template aims to be a guide for the development of reproducible BovReg bioinformatic analyses. Since WP3 standard 
pipelines will be built on top of the analyses previously performed by other packages, the aim of these guidelines is to 
provide a set of minimum good practices to enable that the results obtained by our partners can be reproduced by the 
standard pipelines. To this end, we created a series of templates using [Jupyter](http://jupyter.org/) notebooks 
that you can adapt to share your own pipelines.

The templates run an RNA-seq toy pipeline inspired by the [rnaseq-nf](https://github.com/nextflow-io/rnaseq-nf) demo 
using [Salmon](https://combine-lab.github.io/salmon/).

To reproduce the results yielded by your analysis (and test that our standard pipelines are working as expected) we will
need that you record the following details:

1. [Software](#sw)

    a. [Third-party software](#thirdPartySoftware)

    1. [Docker](#docker)
    
    2. [Singularity](#singularity)

    3. [Conda environment](#conda)

    b. [Custom scripts](#scripts)
    
2. [Workflow](#workflow)

3. [Data](#data)

    a. [Test input data set](#input_data)

    b. [Test output result](#output_data)

4. [An integral solution: Workflow managers](workflow_managers)

**TODO**: **Put also in our first example we deploy the pipeline as a bash script** 

## <a name="sw"></a> 1. Software

Most of the times, to reproduce a computational result it is necessary to run exactly the same versions of the software 
originally used. For this reason, it is convenient to track any piece of software that is used in your analysis and 
this involve both third-party software and your own custon scripts and commands.       

### <a name="thirdPartySoftware"></a> 1.a Third-party software

With the term "third-party software", we refer to all the tools that are used in a bioinformatic analysis and
that are develop by a different organization other than the original development group of the workflow. To trace the 
versions of the programs used in your analyses, we recommend using an environment management system such as 
[Conda](https://docs.conda.io/projects/conda/en/latest/) or a containerization software such as 
[Docker](http://www.docker.com) or Singularity [Singularity](http://singularity.lbl.gov/). Any of these solutions can 
be used to sandbox software tools along with its dependencies, thus, enabling anyone to reproduce your results by 
running exactly the same computational environment. Although you can create your own containers, an additional 
advantage of this approach is that many bioinformatic tools are already available as pre-build containers in public 
repositories. You can download ready-to-run containers from the 
[Biocontainers](https://biocontainers-edu.biocontainers.pro/en/latest/index.html) project. These community releases 
containers for bioinformatics tools in the three above-mentioned flavours (Conda, Docker and Singularity).

---
**NOTE**

If you don't want to use any of the proposed solutions, as a minimum requirement to allow us reproduce your results, 
you should note the name and the versions of the programs used in your workflow. 

---

#### <a name="docker"></a> 1.a.1 Docker

In our template, all the software that is needed to run the pipeline can be found as a [Docker](http://www.docker.com) 
image on DockerHub [here](https://hub.docker.com/r/cbcrg/bovreg-demo/). To generate a Docker image all the instructions 
must be structured in a Dockerfile as explained 
[here](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/). Our image has been created using 
this [Dockerfile](https://github.com/nextflow-io/rnaseq-nf/docker/Dockerfile). 

---
**NOTE**

We also provide an example of how to use biocontainers to run the pipeline using nextflow. If you want to see the 
containers go to the config.  See the 
[biocontainers profile](https://github.com/BovReg/BovReg-Reproducibility/blob/c11643a323cc9d8e7d6b21911c1cc43f86133e9a/rnaseq-nf/nextflow.config#L39-L55)  
inside the `nextflow.config` file. 

---

#### <a name="singularity"></a> 1.a.2 Singularity

Unlike Docker, Singularity can be run without root privileges, a key feature that makes it a more suitable container 
engine in shared HPC environments. The good news is that Docker containers can be run with Singularity (see 
[here](https://sylabs.io/guides/3.5/user-guide/singularity_and_docker.html) for more information). The Docker image on 
our example has been tested to be compatible with Singularity. 

#### <a name="conda"></a> 1.a.3 Conda environment

We also sandbox the software used in our template in a 
[YML file](https://github.com/nextflow-io/rnaseq-nf/conda.yml). This file can be used to 
[generate the Conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) 
to run our example pipeline.  

### <a name="scripts"></a> 1.b Custom scripts

It will convenient that you share any custom script that you have used on your workflow with us. To reproduce your 
results, we will need the exact version of the script that you ran. If you keep your scripts in a version control 
system (such as GitHub, GitLab or other similar solutions), please point us to the state of the code that generate your
results. We show   **TODO: Example of how to do this in the jupyter notebook with a `wget`.** 

## <a name="workflow"></a> 2. Workflow

When performing a bioinformatic analysis a series of interrelated steps are orchestrated to obtain a final result 
starting from the input raw data. Such a sequential set of steps is known as an analysis workflow. To reproduce the 
results yielded by an analysis workflow it is important to keep track of your workflow steps. Importantly, to reach the 
same computational output is not only enough to record the main tools executed in a workflow but also keep track of the 
parameters used for its execution, single commands, ad-hoc script or intermediary formatting step performed. That is why
this template showcases how to record all the commands used in your analysis using a [Jupyter](http://jupyter.org/) 
notebook. 

## <a name="data"></a> 3 Data

To test that the implementation of the pipeline can reproduce your results it is important that you share with us a 
small sample dataset and the results you expect to generate when you run your analysis.

### <a name="input_data"></a> 3.a Test input data set

The idea is that once we develop the standard pipeline, we can use a minimal dataset to assure that we actually are 
reproducing the same results that you get from your original analysis. In our example, the sample dataset comes along 
with the code in the GitHub [repository](https://github.com/BovReg/BovReg-Reproducibility/rnaseq-nf/data/ggal). Note 
that to reduce the size of your sample dataset you can provide part of a chromosome as a reference and subsampled input 
data.

### <a name="output_data"></a> 3.b Test output result

To check that the pipeline is actually working correctly we will need that you share with us the expected results of 
your analysis when the workflow is run using the sample data using a given set of parameters.

## <a name="workflow_managers"></a> 4. Workflow managers: An integral solution

Workflow managers automatize many of the above discussed points. We show how to deploy our demo pipeline using nextflow.
  

TODO: parameters for software --> jupyter notebook or nextflow

## Pipeline

The templates run an RNA-seq toy pipeline inspired by the [rnaseq-nf](https://github.com/nextflow-io/rnaseq-nf) demo 
using [Salmon](https://combine-lab.github.io/salmon/) and includes the following steps:

* Index transcriptome (Salmon)

* Quantifies transcripts, Maps RNA-seq reads (Salmon)

* Quality of RNA-seq data (FastQC)

* Generates HTML report with quality stats from FastQC and Salmon (MultiQC)

## Notebooks

The index jupyter notebook can be found [here](notebook/00_BovReg_notebook_template.ipynb).


**From here this is just a draft**


Since we know that not all of you are using workflow managers, although we strongly advise to use them, we implemented 
two notebooks one which shows how to naively run the workflow and a second one that is run using Nextflow as workflow 
manager.

## How to use this template

Using nextflow, docker and bla, bla

Naive execution

## Funding

BovReg project has received funding from the European Union’s Horizon 2020 research and innovation program under Grant 
Agreement ID. [815668](https://cordis.europa.eu/project/id/815668).








## Drafts **to delete**
 nextflow demo that performs 
A basic pipeline for quantification of genomic features from short read data implemented with Nextflow.

TODO: add this --> If you don't have it already install Docker in your computer. Read more here.
https://docs.docker.com/