### Using CheckM2 on long prokaryotic contigs

The easiest way to filter out long (>300 kb) erroneous prokaryotic contigs is to run [CheckM2](https://github.com/chklovski/CheckM2) on individual contigs. 

If a chimeric contig is long enough, it will often have high CheckM contamination due to the presence of duplicated marker genes from multiple organisms. 

To extract all contigs of length >= X bp and run CheckM2, you can do (with [mylotools](qc.md#mylotools---scripts-for-myloasm-outputs))

```sh 
cd myloasm_results
mylotools extract-contigs --output-folder contigs_dir --min-contig-length X
checkm2 predict --input contigs_dir -x fa -o checkm2_results --threads 40
```
### Using k-mer multiplicity statistics for duplicates/strain chimeras

Myloasm's [fasta outputs](output.md) have information about how often 21-mers are repeated (its multiplicity) within a contig: 

> \>u123123ctg_XXX_**duplicated-yes mult=2.00** <- fasta record with k-mer multiplicity and duplication status.

In our experience, *prokaryotic* contigs should almost always have average k-mer multiplicity near 1.00. If you have a very long contig (> 1M bp) of multiplicity > 1.05, it may be a chimera from multiple strains of a species. We set `duplicated` to `yes` or `possibly` then the multiplicity is high. 

**For small genomes (e.g. viruses)**, the expected k-mer multiplicity may deviate from 1.00. However, a small contig with k-mer multiplicity >> 1 can be suspicious. A contig with k-mer multiplicity = 2, 3, or an integer multiple can indicate a perfectly duplicated contig. 

### Notes on circularized contigs

For prokaryotic genomes, low CheckM2 completeness can indicate premature circularization. However: 

- we have found that complete *organelle* genomes (mitochondria, plastids from microeukaryotes) can have non-trivial CheckM2 completeness (> 30% but < 90%) 
- *secondary chromosomes* and genomes with multiple chromosomes can have lower completeness
- some clades of microbes have low CheckM2 completeness scores, even when they're complete

The myloasm tag `circular-possibly` indicates lower confidence circular genomes (due to low coverage or assembly graph ambiguity), but these can often be complete genomes, especially if CheckM2 scores are good. 
