# Deep-Neural-Networks-in-Genomics

This project is a continuation of my internship at the Amsterdam Genome Diagnostics. Here I'll implement a WGS variant calling pipeline using Nextflow (or Pycharm) and containing the vg Giraffe mapping toolkit and DeepVariant variant caller docker solution. This solution will be plug-and-play for as much as possible from FASTQ file to VCF containing variant calls. It should be runnable on Linux Ubuntu build 20.04 and newer.

This build will include options to tune and train DeepVariant from scratch. This is in order to fine-tune the model to specific requirements. However, the default will be sufficiently performant for most variant calling applications.

## Requirements
- Unix or Mac operating system, or WSL for windows
- Python >3.10
- Java >17
- Docker
- A package manager conda / uv, I'll be using uv
- GPU (optional)
- requirements can be installable separately

## Getting Started
### vg (Giraffe) packages
Variation graphs, vg, provide encoding of sequences of the genome. This is preferable as this speeds up the mapping process significantly over alignemnt of symbols, A, G, T, C. This model is similar to sequence graphs that have been used in assembly and multiple sequence alignment.

https://github.com/vgteam/vg

We build the dependencies by cloning the vg repo and installing the dependencies.

```
git clone --recursive https://github.com/vgteam/vg.git
cd vg
```

In vg directory.

```
make get-deps
```

After which we can build vg

```
make
```

Building the binary inside the vg repository.

```
./bin/vg

echo 'export PATH="${PATH}:'"$(pwd)"'/bin"' >>~/.bashrc
```


May take a while.

vg uses multiple CPU cores, making paralization possible. It's smart to check how much cores you have available as this influences runtime significantly.

```
nproc -all 
```
Use make j16 to run 16 build threads at a time, which greatly accelerates the process. More CPU cores, more better. Can take any time from 10 minutes to 1 hour. This is a heavy build, allocate resources accordingly to prevent an OOM kill.

```
make -j$(nproc) // Use all cores
```
Run using `./bin/vg` or add to path to run using `vg` in the future.

```
echo 'export PATH="${PATH}:'"$(pwd)"'/bin"' >>~/.bashrc
```

### Deploying DeepVariant through Docker
We deploy the deepvariant model using Docker, which is the recommended method by the Google Team.

https://github.com/google/deepvariant/blob/r1.10/docs/deepvariant-quick-start.md

### Configuring Nextflow
Using Nextflow to create a scalable, portable and reproducable workflow is very important. Nextflow supports a range of compute environments, making it a usefull tool. At the time of writing it is a very active community.

Note: nextflow is installable using conda as well.

https://docs.seqera.io/nextflow/install

### hap.py for genomic evaluation
Evaluation tool for assessing variant calling accuracy. Usually done by means of comparing to the golden standard.

### MLFlow for retraining (optional)
Widely adopted AIOps framework that can work with virtually any machine learning framework, including Tensorflow, which is what DeepVariant is based on.

### Variant Interpretation using Alphagenome
Deepmind's AlphaGenome model can decipher the regolatory code within DAN sequences. Offering multimodel predictions to the goal of predicting gene expresion, splicing patterns, chromatin features and contact maps. 

## References
Thanks to all different groups and contributors that have made these types of analysis possible! Specifically I refer to the papers of DeepVariant, vg, and Nextflow.

- DeepVariant: A universal SNP and small-indel variant caller using deep neural networks. Nature Biotechnology 36, 983–987 (2018).
Ryan Poplin, Pi-Chuan Chang, David Alexander, Scott Schwartz, Thomas Colthurst, Alexander Ku, Dan Newburger, Jojo Dijamco, Nam Nguyen, Pegah T. Afshar, Sam S. Gross, Lizzie Dorfman, Cory Y. McLean, and Mark A. DePristo.
doi: https://doi.org/10.1038/nbt.4235
- vg: Jouni Sirén, et al. Pangenomics enables genotyping of known structural variants in 5202 diverse genomes.Science374,abg8871(2021).DOI:10.1126/science.abg8871
- Nextflow: P. Di Tommaso, et al. Nextflow enables reproducible computational workflows. Nature Biotechnology 35, 316–319 (2017) doi:10.1038/nbt.3820
- hap.py: 
- MLFlow: 
- AlphaGenome: Avsec, Ž., Latysheva, N., Cheng, J. et al. Advancing regulatory variant effect prediction with AlphaGenome. Nature 649, 1206–1218 (2026). https://doi.org/10.1038/s41586-025-10014-0

