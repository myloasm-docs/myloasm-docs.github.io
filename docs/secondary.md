```
├── myloasm_(DATE + TIME).log
├── assembly_graphs/
│   ├── unitig_graph-0.gfa
│   ├── after_light_cleaning-1.gfa
│   ├── after_walk_heavy_cleaned-2.gfa
│   └── small_and_tip_bubble-3.gfa
├── 0-cleaning_and_unitigs/
│   └── Read cleaning + mapping files
├── 1-light_resolve/
│   └── Initial graph cleaning files
├── 2-heavy_path_resolve/
│   └── Heavy graph cleaning files
├── 3-mapping/
│   └── map_to_unitigs.paf.gz
├── binary_temp/
│   └── Large binary files 
└── alternate_assemblies/
    ├── duplicated_contigs.fa
    └── assembly_alternate.fa
```

### `myloasm_*.log`

Logging information. Has some extra information over just the stderr output. 

### `assembly_graphs/`

Contains intermediate assembly graphs in GFA format. [See here for more info about myloasm's GFA outputs.](output.md#the-final-assembly-graph-final_contig_graphgfa). 

- `unitig_graph-0.gfa` - raw unitigs with minimal cleaning. Usually extremely messy. 
- `after_light_cleaning-1.gfa` - lightly cleaned unitigs after removing relatively small overlaps
- `after_walk_heavy_cleaned-2.gfa` - heavily cleaned unitigs after using coverage information.
- `small_and_tip_bubble-3.gfa` - further cleaning of tips and rescuing some small circular contigs

### `0-cleaning_and_unitigs/`

These are files during the initial read-to-read mapping, read containment, and graph construction steps. 

- `all-cont.txt.gz` - containment status of all reads
- `overlaps.txt.gz` - information about overlaps between non-contained reads
- `read_coverages.txt.gz` - this file gives information about reads that are chimeric and where they get split
- `remap_temp/` - we do multiple rounds of splitting and overlapping; these files are for the second round. 

### `1-light_resolve/`

These files show intermediate assembly graphs during the initial, light graph cleaning iterations. 

### `2-heavy_path_resolve/`

These files show intermediate assembly graphs and information about the inferred edge weights during the heavier graph cleaning iterations. 

The graphs look like: `heavy-m15-t0.5-r0.5.gfa`. Here, larger `m` indicates larger topological graph simplifications. `t` is the temperature (lower is more aggressive). `r` is the edge weight cut ratio (higher is more aggressive). 

### `3-mapping/`

These files show how read (or contigs) map to the final unpolished contigs. We use "unitigs" and "contigs" interchangeably here. 

- `map_to_unitigs.paf.gz` - mapping of reads to unpolished unitigs in [PAF format](https://lh3.github.io/minimap2/minimap2.html#10). There are additional columns indicating some SNP information. 
- `dereplicate_unitigs.paf.gz` - we map intermediate unitigs to other unitigs and filter out unitigs that map perfectly, prior to polishing. 

### `binary_temp/`

These are large binary files that are dumped by myloasm. This is useful for rerunning myloasm after a failure by doing `myloasm -o output_dir exist` -- note the magic keyword `exist`. 

If you don't want these files to be output, use the `--clean-dir`. 

### `alternate_assemblies/`

- If a contig is > 99.9% similar and contained in another contig, it is put into `duplicated_contigs.fa`. 

- If a contig is > 99% similar but < 99.9% similar and contained in other contigs, we put it into `assembly_alternate.fa`. 
