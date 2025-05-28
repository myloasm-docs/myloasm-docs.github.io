## Conda install (x86-64 + AVX2 instructions)

```sh
mamba install -c bioconda myloasm
```

## Portable x86-64 + AVX2 binary

```sh
wget https://github.com/bluenote-1577/myloasm/releases/download/v0.1.0/myloasm-0.1.0-x86_64-avx2
chmod +x myloasm-0.1.0-x86_64-avx2
./myloasm-0.1.0-x86_64-avx2
```

- This binary is not static but dynamically linked to older version of shared libraries (GLIBC and GLIBCXX) built on CentOS 7.
- Requires AVX2 instructions and x86-64 architectures (most linux machines). 

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

###  SSE2 but no AVX2 instructions 

```sh
cargo install --path . --features=sse --no-default-features
```

### ARM NEON instructions 

!!! warning

    Compilation should work on ARM architectures supporting NEON instructions. However, runtime performance may significantly degrade for the polishing step.

```sh
cargo install --path . --features=neon --no-default-features
``` 
