 <img src='assets/logo.svg' width='90%' />

Myloasm is a *de novo* metagenome assembler for long-read sequencing data. It takes sequencing reads and outputs polished contigs in a single command. 


**Myloasm works with:**

- Nanopore R10 simplex reads with > ~97% accuracy (basecalled in *sup* or *hac* mode)
- PacBio HiFi reads

**Installation and Usage:** See the [Install](install.md) and [Usage](usage.md) sections on the navigation side bar. Source code is available at the [GitHub repo.](https://github.com/bluenote-1577/myloasm)

## Why myloasm?

**Results**: [Here are some preliminary results for myloasm](results.md) until the preprint officially comes out.

**Philosophy**: Myloasm was designed to take advantage of modern long reads. Even the noisiest modern long reads (e.g., nanopore simplex R10) have become quite accurate—myloasm uses a new approach that enables high-resolution assembly from this data.

**Strengths:** myloasm can 

- often assemble similar (intraspecies) *strains* better than other nanopore assemblers
- take advantage of very long reads better than de Bruijn graph approaches
- obtain contiguous assemblies in even complex, highly heterogeneous metagenomes

**Limitations:** myloasm may

- occasionally produce chimeric misassembled contigs due to its aggressiveness.
    - we provide extra debugging information for manual curation; see [the quality control guide](qc.md).
- use more memory than other assemblers. Currently, a ~200 gigabase long-read human gut sample takes ~450 GB of RAM. 


 

## Issues, questions, and discussions

- Found a bug or have an issue? Go to https://github.com/bluenote-1577/myloasm/issues 
- Have a general question or discussion topic? Go to https://github.com/bluenote-1577/myloasm/discussions

## Citation

Jim Shaw and Heng Li. Forthcoming. 
