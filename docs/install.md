Myloasm can be installed in three ways. 

1. [Bioconda](https://bioconda.github.io/)
2. Executable binary
3. Building from source (mandatory if on ARM architectures)

## Conda install (x86-64 + AVX2 instructions)
[![Anaconda-Server Badge](https://anaconda.org/bioconda/myloasm/badges/version.svg)](https://anaconda.org/bioconda/myloasm)
[![Anaconda-Server Badge](https://anaconda.org/bioconda/myloasm/badges/latest_release_date.svg)](https://anaconda.org/bioconda/myloasm)

```sh
mamba install -c bioconda myloasm mylotools
```

This installs both (1) myloasm and (2) [mylotools](mylotools.md), a set of utilities for visualizing and manipulating myloasm's outputs. The other methods below do not install mylotools. 

## Portable x86-64 + AVX2 binary

```sh
wget https://github.com/bluenote-1577/myloasm/releases/download/v0.4.0/myloasm-0.4.0-x86_64-avx2
chmod +x myloasm-0.4.0-x86_64-avx2
./myloasm-0.4.0-x86_64-avx2
```

- This binary is not static but dynamically linked to older version of shared libraries (GLIBC and GLIBCXX) built on CentOS 7.
- Requires AVX2 instructions and x86-64 architectures (most linux machines). 

## Build from source

**Requirements**:

* [Rust programming language](https://www.rust-lang.org/) >= v1.85
* gcc 4.8+ or clang 3.4+
* cmake 3.5+

### x86-64 linux systems with AVX2 (most modern machines)

Compiling from source should take a few minutes.

```sh
git clone https://github.com/bluenote-1577/myloasm --recurse-submodules  
cd myloasm
cargo install --path . 
myloasm -h
```

###  SSE2 but no AVX2 instructions 

```sh
cargo install --path . --features=sse --no-default-features
```

### ARM NEON instructions 

```sh
cargo install --path . --features=neon --no-default-features
``` 
