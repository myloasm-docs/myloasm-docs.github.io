 <img src='assets/logo.svg' width='90%' />

Myloasm is a *de novo* metagenome assembler for long-read sequencing data. It takes sequencing reads and outputs polished contigs in a single command. 


**Myloasm works with:**

- Nanopore R10 simplex reads with > ~97% accuracy (basecalled in *sup* or *hac* mode)
- PacBio HiFi reads

## Why myloasm?

Myloasm was designed to take advantage of modern long reads. The main idea is that even the noisiest modern long reads (e.g., nanopore simplex R10) have become quite accurate. Myloasm uses a new approach that enables high-resolution assembly from this data.

**Strengths:** myloasm can 

- assemble similar (intraspecies) *strains* better than other nanopore assemblers
- take advantage of very long reads better than de Bruijn graph approaches
- obtain contiguous assemblies in even complex, highly heterogeneous metagenomes

**Limitations:** myloasm may

- occasionally produce chimeric misassembled contigs due to its aggressiveness.
    - we provide extra debugging information for manual curation; see [the quality control guide](qc.md).
- use more memory than other assemblers. Currently,  a ~200 gigabase long-read human gut sample takes ~450 GB of RAM.

## Algorithm outline

At a high level, myloasm uses a [string graph](https://academic.oup.com/bioinformatics/article/21/suppl_2/ii79/227189) approach. Myloasm disentangles the overlap graph using polymorphic, strain-specific k-mers. Myloasm then finds walks along the simplified graph with consistent coverage to obtain the final contigs. 

