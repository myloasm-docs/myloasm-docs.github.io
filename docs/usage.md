### Nanopore R10.4 (sup/hac basecalling)

```sh
myloasm reads1.fq reads2.fq reads3.fq -o output_directory -t 50
```

- Positional inputs are reads. Multiple reads are concatenated. Myloasm uses base qualities, so fastq files are preferred over fasta.
- `-o`: results directory; a new directory is made if not present.
- `-t`: number of threads

### PacBio HiFi

```sh
myloasm reads1.fq reads2.fq reads3.fq -o output_directory -t 50 --hifi
```

- `--hifi`: append the HiFi flag is using HiFi reads. Everything else is the same. 

## Useful common parameters

- `--clean-dir` - myloasm dumps large intermediate files to the results directory by default to enable rerunning from intermediate failure. Specify this flag to not dump these large files. 
- `--min-reads-contig` - myloasm outputs all contigs, even those with a single read, by default. Increase to retain only contigs with >= X reads. 
- `-c` - increase this to reduce memory and increase speed with some sensitivity loss. Should be <= 15.
- `--quality-value-cutoff` - myloasm retains reads with only >= X estimated accuracy for graph building. Increasing may create more accurate assembly graphs at a loss of sensitivity. 
- `--min-ol` - Allow overlaps of length >= X for assembly graph construction. The default is quite aggressive and more sensitive at low coverage, but may lead to more false positives. Consider increasing for more accuracy for high coverage contigs. 
- `--bloom-filter-size` - The Bloom filter size in GB. Myloasm uses a bloom filter for reducing memory during the k-mer counting stage. Consider increasing for large metagenomes (> 100 Gbp)
- `--aggressive-bloom` - Use a more aggressive Bloom filtering strategy. Makes results non-deterministic, but saves some memory during initial k-mer counting step.



