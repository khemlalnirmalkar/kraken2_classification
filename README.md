# Kraken2 classification
Short read classification with the kraken2 program

## Introduction
[Kraken2](http://ccb.jhu.edu/software/kraken/) is a short read classification system that is fast and memory efficient. It allows you to assign a taxonomic identification to each read from a sequencing run. Kraken assigns each read to the lowest commen ancestor (LCA) of all sequences it alignes to. Through the use of the Bracken package, you can also get accurate estimates of proportions of different species. This guide will cover some of the basics, but the full [manual](http://ccb.jhu.edu/software/kraken/MANUAL.html) is quite good and has more detail.

## Table of contents
1. [Installation](manual/installation.md)
2. [Usage](manual/usage.md)
3. [Available databases](manual/databases.md)
4. [Downstream processing and plotting](manual/downstream_plotting.md)
5. [Additional considerations](manual/extra.md)

## Quickstart
*Install*
```
conda env create -f classification_env.yaml
```
*Run*
```
# Shell command
DB=/labs/asbhatt/data/program_indices/kraken2/kraken_custom_oct2018/genbank_bacteria
read_length=150   # must be 150 or 100
kraken2 --db "$DB" --threads 2 --output out.krak --report out.krak.report --paired r1.fq r2.fq
bracken -d "$DB" -i out.krak.report -o out out.krak.report.bracken -r "$read_length"
# Snakemake workflow 
source activate classification2
snakemake -s path/to/Snakefile --configfile config.yaml
```

## Parsing output reports
The Kraken reports (sample.krak.report) and bracken reports (sample.kraK_bracken.report) are the best for downstream analysis. See [Downstream processing and plotting](manual/downstream_plotting.md) for details on using the data in R. 