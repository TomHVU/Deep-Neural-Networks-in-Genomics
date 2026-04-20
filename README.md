# Deep-Neural-Networks-in-Genomics

This project is a continuation of my internship at the Amsterdam Genome Diagnostics. Here I'll implement a WGS variant calling pipeline using Nextflow (or Pycharm) and containing the vg Giraffe mapping toolkit and DeepVariant variant caller docker solution. This solution will be plug-and-play for as much as possible from FASTQ file to VCF containing variant calls. It should be runnable on Linux Ubuntu build 20.04 and newer.

This build will include options to tune and train DeepVariant from scratch. This is in order to fine-tune the model to specific requirements. However, the default will be sufficiently performant for most variant calling applications.

## Requirements
- Unix-like operating system, or WSL-type solutions
- Python >3.10
- Java >17
- Docker
- A package manager conda / uv, I'll be using uv
- GPU (optional)

## Getting Started
### Getting vg Giraffe packages
Variation graphs, vg, provide encoding of sequences of the genome. This is preferable as this speeds up the mapping process significantly over alignemnt of symbols, A, G, T, C. This model is similar to sequence graphs that have been used in assembly and multiple sequence alignment.

https://github.com/vgteam/vg

### Deploying DeepVariant through Docker
We deploy the deepvariant model using Docker, which is the recommended method by the Google Team.

https://github.com/google/deepvariant/blob/r1.10/docs/deepvariant-quick-start.md

### Configuring Nextflow
Using Seqera's Nextflow to create a scalable, portable and reproducable workflow is very important. Nextflow supports a range of compute environments, making it a usefull tool. At the time of writing it is a very active community.

https://docs.seqera.io/nextflow/install

## References
Thanks to all different groups and contributors that have made these types of analysis possible! Specifically I refer to the papers of DeepVariant, vg, and Nextflow.

A universal SNP and small-indel variant caller using deep neural networks. Nature Biotechnology 36, 983–987 (2018).
Ryan Poplin, Pi-Chuan Chang, David Alexander, Scott Schwartz, Thomas Colthurst, Alexander Ku, Dan Newburger, Jojo Dijamco, Nam Nguyen, Pegah T. Afshar, Sam S. Gross, Lizzie Dorfman, Cory Y. McLean, and Mark A. DePristo.
doi: https://doi.org/10.1038/nbt.4235
Jouni Sirén, et al. Pangenomics enables genotyping of known structural variants in 5202 diverse genomes.Science374,abg8871(2021).DOI:10.1126/science.abg8871
P. Di Tommaso, et al. Nextflow enables reproducible computational workflows. Nature Biotechnology 35, 316–319 (2017) doi:10.1038/nbt.3820