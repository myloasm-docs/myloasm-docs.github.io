#### Question not answered below?

Open up an [issue](https://github.com/bluenote-1577/myloasm/issues) or a [discussion](https://github.com/bluenote-1577/myloasm/discussions).

## Is there a way to resume an incompleted myloasm run?

**Yes**. The `binary_temp` files in the results directory contain intermediate checkpoint files. You can rerun from these checkpoints using the `exist` keyword. 

```sh
myloasm exist -o results_directory (options)`
```

## What read-level quality control does myloasm do? Do you need to do QC?

Myloasm removes reads with < 1kbp and < X% mean base quality; X is taken from `--quality-value-cutoff` (default = 90) using the fastq. **Adapters are not removed from the reads**. 

Adding more stringent filters is fine (e.g., filtering > 99% base quality). This could improve the assembly at the cost of losing lower coverage stuff / lower contiguity.


## What are the polishing warnings in the output log? 

See [the answer here](https://github.com/bluenote-1577/myloasm/issues/9). Basically, polishing is often far from perfect in real metagenomes. Myloasm detects when there are some issues and spits it out into the log. We don't do much with these warnings as of v0.3.0 (this may change). 

## Why are there super long contigs > 10 Mbp in my output file?

These are probably chimeras (erroneously joined contigs). See [mylotools](mylotools.md) for tools to inspect contigs to see if these have good coverage/read overlaps. But these could in theory be eukaryotic genomes too.

## Does myloasm work on isolate bacteria + plasmids / human / non-metagenomes?

- *Isolate bacteria and plasmids*: [Ryan Wick benchmarked myloasm and it works pretty well](https://rrwick.github.io/2025/09/23/autocycler-benchmark-update.html) on isolate bacteria ONT metagenomes. Make sure to use the newest versions. 

- *Human and complex eukaryotic genomes*: Probably not. Myloasm can't handle very complex, low-entropy sequences as well as other long-read assemblers. 

- *Simpler eukaryotes*: Eukaryotes with simpler genomes should be roughly okay. Telomeric sequences and long homopolymers are generally difficult for ONT reads though; [see here](https://rrwick.github.io/2025/09/04/homopolymer-polishing.html).

## Does myloasm work with fasta reads?

**Yes**. Myloasm does use quality scores for a few tasks (e.g., polishing, SNPmer calling), so the results may be slightly worse. But fasta is usable. 


## What about duplicated read IDs?

Duplicated read IDs are fine. 