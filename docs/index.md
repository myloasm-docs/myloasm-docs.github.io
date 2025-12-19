 <img src='assets/logo.svg' width='90%' />

Myloasm is a *de novo* metagenome assembler for long-read sequencing data. It takes sequencing reads and outputs polished contigs in a single command. 


**Myloasm works with modern long reads such as:**

- Nanopore R10 simplex reads with > ~97% accuracy (basecalled in *sup* or *hac* mode)
- PacBio HiFi reads

**Installation and Usage:** See the [Install](install.md) and [Usage](usage.md) sections on the navigation side bar. Source code is available at the [GitHub repo.](https://github.com/bluenote-1577/myloasm)

!!! Important
    Version 0.3.0 was released December 19, 2025. See [CHANGELOG](CHANGELOG.md) for more information.

## Why myloasm?

**Results**: [Here are some preliminary results for myloasm](results.md); see the preprint for more details. 

**Philosophy**: Myloasm was designed to take advantage of modern long reads. Even the noisiest modern long reads (e.g., nanopore simplex R10) have become quite accurate. Myloasm uses a new algorithmic framework that enables high-resolution assembly from this data.

**Strengths:** myloasm can 

- often assemble similar (intraspecies) *strains* better than other nanopore assemblers
    - we have found that other nanopore assemblers collapse similar genomes at > 95% [ANI](https://www.nature.com/articles/s41576-025-00911-5)—whereas myloasm can resolve up to 99% ANI quite confidently.
- obtain contiguous assemblies in diverse metagenomes from human gut to soil
- myloasm uses about the same RAM as metaFlye with faster runtime

**Limitations:** myloasm may

- occasionally produce chimeric misassembled contigs (like all metagenome assemblers)
    - we provide [tools for quality control and visualization](mylotools.md); also see [the quality control guide](qc.md).
- use more RAM than sparse minimizer approaches like metaMDBG.


## Issues, questions, and discussions

- Found a bug or have an issue? Go to https://github.com/bluenote-1577/myloasm/issues 
- Have a general question or discussion topic? Go to https://github.com/bluenote-1577/myloasm/discussions

## Citation

[Jim Shaw, Maximillian Marin, and Heng Li. High-resolution metagenome assembly for modern long reads with myloasm. bioRxiv (2025).](https://www.biorxiv.org/content/10.1101/2025.09.05.674543v1)
