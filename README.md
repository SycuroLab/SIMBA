# SIMBA

<p align="center">
SInthetic MicroBiome Analysis - a program that analyzes synthetic/contrived/designed microbiome dynamics, enrichment and community changes
</p>

<div align="center">
<img width="300" height="300" alt="ChatGPT Image May 21, 2026, 10_24_39 AM" src="https://github.com/user-attachments/assets/c3f69829-1697-40d0-ab50-b94b38899ef5" />
</div>

This is a snakemake workflow for profiling and analyzing synthetic and/or designed microbial communities from amplicon sequencing data using various programs designed for microbiome analysis, including and not limited to the Prokka, eggNOG-mapper, the Divisive Amplicon Denoising Algorithm 2 (DADA2), Phylogenetic Investigation of Communities by Reconstruction of Unobserved States (PICRUSt2), the Microbe Multivariable Associations with Linear Models (MaAsLin2), amongst others.

Unlike existing software relying on public databases, SIMBA allows the user to include their assembled genomes for annotation and increase the precision of functional prediction calls.

The DADA2 tutorial can be found from https://benjjneb.github.io/dada2/index.html. The initial code was cloned from https://github.com/SilasK/amplicon-seq-dada2 and heavily modified to make this workflow suitable for our needs. The PICRUSt2 tutorial can be found in https://huttenhower.sph.harvard.edu/picrust/. The MaAsLin2 tutorial is avalable in https://huttenhower.sph.harvard.edu/maaslin2/. 

In this pipeline, species-level taxonomy assignment is performed using two complementary methods: DADA2 and VSEARCH and incorporates annotations from the user's database and also GTDB.

Some of the changes and parameters included in this program are as follows:

1- DADA2: it uses a naive Bayesian classifier method (https://pubmed.ncbi.nlm.nih.gov/17586664) combined with a strict 100% nucleotide identity requirement between query ASVs and reference sequences. In this pipeline, four databases were used during the DADA2 classification step; however, for the final taxonomy, we retained GTDB-based assignments, and when GTDB did not provide an annotation for an ASV, we fell back to the corresponding URE annotation.

2- VSEARCH: it is an open-source alternative to USEARCH that performs optimal global sequence alignments between query ASVs and reference sequences at user-defined identity thresholds (supports adjustable (non-100%) identity thresholds). For a more comprehensive understanding of this methodology, please refer to the paper available at https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5075697/ and the manual at https://github.com/torognes/vsearch/releases/download/v2.27.0/vsearch_manual.pdf. In this pipeline, VSEARCH classifications were generated using the GTDB database, and when GTDB lacked species information for a given ASV, the corresponding URE annotation was used instead.

When integrating taxonomy assignments from VSEARCH and DADA2, we prioritized VSEARCH-derived annotations over the DADA2 RDP classifications, and GTDB-based annotations over those obtained from the field-specific URE database. In cases where the taxonomy_final entry originated from VSEARCH but the species (spp) field was missing (NA), we substituted the corresponding DADA2 species-level annotation. This strategy leverages the strengths of both methods and both databases, resulting in more complete and accurate taxonomic assignments across ASVs.

At the end of the workflow, we generate two versions of taxonomy annotation files, allowing users to choose the format that best fits their downstream analysis:

dada2_all_databases_merged.csv Contains taxonomic annotations from all databases side by side (e.g., GTDB, SILVA, RDP, uRE), without combining or prioritizing them. This file is useful for users who want to compare database outputs directly.

vsearch_dada2_merged.tsv Provides a single, merged annotation per ASV by combining VSEARCH and DADA2 results from two main databases: the GTDB reference database and a vaginal field-specific database (URE).
## Installation

## Input files

SIMBA requires the following:

- A path to your directory where your annotated genomes are located
- A file with your sample names (i.e. sample_list.txt)
- A file with the copy number variation of the 16S gene (i.e. 16S_count.txt)
- An ASV count table where the columns are the sample names (the sample names must match the file with your samples)

## Output files
