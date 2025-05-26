## Conda install (forthcoming)

```sh
mamba install -c bioconda myloasm
```

## Build from source

**Requirements**:

* [Rust programming language](https://www.rust-lang.org/) >= v1.81
* gcc 4.8+ or clang 3.4+
* cmake 3.5+

### x86-64 linux systems with AVX2 (most modern machines)

```sh
git clone https://github.com/bluenote-1577/myloasm --recurse-submodules  
cd myloasm
cargo install --path . 
myloasm -h
```

### Other systems (non AVX2 + x86-64 systems)

####  SSE2 but no AVX2 instructions 

```sh
cargo install --path . --features=sse --no-default-features
```

#### ARM NEON instructions 

!!! warning

    Compilation should work on ARM architectures supporting NEON instructions, but I offer no guarantees on the runtime performance, which may degrade for the polishing step.

```sh
cargo install --path . --features=neon --no-default-features
``` 