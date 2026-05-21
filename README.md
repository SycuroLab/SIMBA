# SIMBA

<p align="center">
SInthetic MicroBiome Analysis - a program that analyzes synthetic/contrived/designed microbiome dynamics, enrichment and community changes
</p>

<div align="center">
<img width="300" height="300" alt="ChatGPT Image May 21, 2026, 10_24_39 AM" src="https://github.com/user-attachments/assets/c3f69829-1697-40d0-ab50-b94b38899ef5" />
</div>

This is a snakemake workflow for profiling and analyzing synthetic and/or designed microbial communities from amplicon sequencing data using various programs designed for microbiome analysis, including and not limited to the Divisive Amplicon Denoising Algorithm 2 (DADA2), Phylogenetic Investigation of Communities by Reconstruction of Unobserved States (PICRUSt2), the Microbe Multivariable Associations with Linear Models (MaAsLin2), amongst others.

Unlike existing software relying on public databases, SIMBA allows the user to include their assembled genomes for annotation and increase the precision of functional prediction calls.

The DADA2 tutorial can be found from https://benjjneb.github.io/dada2/index.html. The initial code was cloned from https://github.com/SilasK/amplicon-seq-dada2 and heavily modified to make this workflow suitable for our needs. The PICRUSt2 tutorial can be found in https://huttenhower.sph.harvard.edu/picrust/. The MaAsLin2 tutorial is avalable in https://huttenhower.sph.harvard.edu/maaslin2/. 

In this pipeline, species-level taxonomy assignment is performed using two complementary methods: DADA2 and VSEARCH and incorporates annotations from the user's database and also GTDB.

## Installation

## Input files

## Output files
