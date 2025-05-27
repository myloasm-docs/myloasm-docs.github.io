# Output directory 

```
myloasm_output 
    ├── assembly_primary.fa <-- CONTIGS
    ├── final_contig_graph.(gfa/edges) <-- GRAPH 
    └── OTHER STUFF (secondary files)
```

- [The main contig file: **assembly_primary.fa**](#the-main-contig-file-assembly_primaryfa)
    * [Contig fasta record label definition](#contig-fasta-record-label-definition)
        + [Circularity](#circularity)
        + [Estimated depth of coverage ](#estimated-depth-of-coverage)
        + [K-mer multiplicity](#k-mer-multiplicity)
- [The final assembly graph: **final_contig_graph.gfa**](#the-final-assembly-graph-final_contig_graphgfa)
    * [Understanding myloasm's GFA assembly graph format ](#understanding-myloasms-gfa-assembly-graph-format)
        + [Contig information ](#contig-information)
         + [Read information ](#read-information)


## The main contig file: **assembly_primary.fa**

These are the main polished contigs to be used for downstream analysis most of the time. 

### Contig fasta record label definition

The fasta records looks like this:

>\>u2658272ctg_len-2275750_circular-possibly_depth-10-9-9_mult-1.00

`u2658272ctg` is the identifier and `len-X` is the length in nucleotides. There is also information about the circularity, depth of coverage, and repetitiveness of the contig. 

#### Circularity

`circular-X`: X is either `yes`, `no`, or `possibly`. 

If a contig has a self loop in the assembly graph and 

1. has average depth > 5x and 
2. has no other connections (i.e., consists of a single node and a single edge) 

then it is `yes`. 

If it has a self loop, but (1) or (2) fails above, then it is `possibly`. Otherwise, it is `no`. 

#### Estimated depth of coverage 

`depth-X1-X2-X3`: This is the estimated depth of coverage.

The three distinct values represent different levels of nucleotide identity thresholds. 

1. `X1` is the depth while allowing alignments of approximately > 99% true nucleotide similarity (estimated using myloasm's SNP + k-mer formulation). 
2. `X2` is the depth for > 99.75% similarity.
3. `X3` is the depth for 100% similarity.

#### K-mer multiplicity

`mult-X`: this is the estimated fraction of repetitiveness and useful for quality control. 

This is estimated by counting 21-mers across the contig and seeing how often they repeat on average after removing the most frequent and least frequent 10% of k-mers. 

- Most complete prokaryotic genomes should have `mult-1.00`. 
- Sometimes myloasm erroneously concatenates two similar strain genomes together. In this case, `mult` is > 1.0 and indicative of contamination. 
- Long reads often contain duplicate plasmids. Sometimes, a plasmid is erroneously duplicated or miscircularized, giving `mult` > 1. 

## The final assembly graph: **final_contig_graph.gfa**

Each contig in `assembly_primary.fa` is a node in the final assembly graph, `final_contig_graph.gfa`. This is in modified [GFA format](https://gfa-spec.github.io/GFA-spec/GFA1.html) and can be visualized with [Bandage](https://rrwick.github.io/Bandage/).

Each `*.gfa` file has a corresponding `*.edges` file. The edges files gives more detailed information about contig-to-contig overlaps. 

### Understanding myloasm's GFA assembly graph format 

Myloasm's GFA file contains a header starting with `H`. Then, there is additional contig + read information that may be useful for manual curation.  

#### Contig information 

```
S       u165592ctg              LN:i:1034269    DP:f:25.0       DP2:f:24.0      DP3:f:23.0      MEDIAN_DP1:f:35.0
```

- **NOTE**: `LN:i` is only an *approximate* length. This is the length **before polishing**.
- `DP`, `DP2`, and `DP3` is the median of all `DP/2/3` values across the reads (see below). [See here for more information on depth](#estimated-depth-of-coverage). 
- `MEDIAN_DP1` is the median-of-the-median-depth across all reads. `DP` is the median-of-the-*minimum*-depth across all reads. You can ignore the difference and use `DP` instead of `MEDIAN_DP1` most of the time. 

####  Read information: 

```
a       u165592ctg,0-28710      165592  0       SRRX.2+split0       -       28710   DP1:22,DP2:22,DP3:21,READ_LEN:43601,OL_LEN_NEXT:14808,SNP_SHARE_NEXT:216,SNP_DIFF_NEXT:1
a       u165592ctg,34-6529      1421634 28710   SRRX.1+split0+split0        +       6495    DP1:42,DP2:42,DP3:13,READ_LEN:21212,OL_LEN_NEXT:14629,SNP_SHARE_NEXT:129,SNP_DIFF_NEXT:0
```

1. `a` indicates this is a read
2. `u165592ctg,0-28710` indicates that positions 0-28710 come from read `SRRX.2+split0` **before polishing**.
3. `165592` is the numeric read id. Myloasm assigns each read as a unique id. 
4. `0` indicates this read's contribution to the unpolished contig starts at position 0
5. `SRRX.2+split0` - Read name. If myloasm thinks a read is chimeric, it may be split into several sub reads. For example, `split1` indicates the second chunk after splitting. Unsplit reads may also be denoted as `+split0`. There are two rounds of chimera splitting. 
6. `-/+` - read orientation

The last columns indicate the depth and overlap information of each read. [See here for more information on varying depth values](#estimated-depth-of-coverage). 

- `OL_LEN_NEXT` - number of overlapping bases to the next read
- `SNP_SHARE_NEXT` - number of estimated shared SNPs to the next read
- `SNP_DIFF_NEXT` - number of estimated different SNPs to the next read. 


