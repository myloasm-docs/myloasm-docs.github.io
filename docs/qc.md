Like all other metagenome assemblers, myloasm can produce erroneous assemblies.

**Chimeric contigs:** chimeric contigs consist of sequences from two or more genomes. This error can happen for a variety of reasons. The most common are:

- long interspecies shared genomic regions (e.g., horizontal gene transfer) can confuse assemblers
- extremely similar strains are hard to resolve, leading to strain-chimeric contigs
- chimeric long-reads due to technical sequencing artifacts can cause downstream errors in assembly

**Duplicated small contigs:** we noticed that long-read assemblers can incorrectly duplicate small sequences (plasmids or viruses). 

The cause isn't always obvious, but we often found that a *single long read* can consist of *multiple copies* of the same plasmid. 

**Prematurely circuarlized contigs:** assemblers can prematurely circularize contigs, i.e., claim contigs are circular even though they are not. Algorithmically, this arises due to genome repeats.



## mylotools - scripts for myloasm outputs

We provide a set of tools for working with myloasm assemblies called **[mylotools](https://github.com/bluenote-1577/mylotools)**. We discuss how to use `mylotools` below for quality control. To install mylotools, do

```sh
git clone https://github.com/bluenote-1577/mylotools
cd mylotools

## assuming you have python3 installed
pip install . 

mylotools -h

## plot and inspect contigs
cd myloasm_results
mylotools plot u32910ctg

ls u32910ctg_analysis.html

```

## Quality control (QC) guides

### Guide 1: QC statistics and interpretation

[See here for some notes on how to obtain and interpret QC statistics from myloasm.](qc_statistics.md)

### Guide 2: Manual inspection of myloasm's outputs with mylotools and decontaminating contigs

[See here for how the `mylotools plot` utility can provide overlap/coverage/GC information.](qc_manual.md)