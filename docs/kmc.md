Myloasm's default k-mer counter holds everything in memory. For large or high-diversity metagenomes (e.g. soil, sediment) this can become the bottleneck. `--kmc` counts k-mers on disk instead, using a separate helper binary. `--kmc` is also usually faster than the default k-mer counter. 

See the [myloasm-kmc repo](https://github.com/bluenote-1577/myloasm-kmc) for install instructions and details.

### Installation

#### Option 1: conda

```sh
conda install -c bioconda myloasm-kmc
```

#### Option 2: build from source

Requirements: very standard unix-based toolchain (should be available by default) + the Rust language. Specifically, 

- a C++14 compiler (GCC 5+ or Clang)
- `zlib.h` - zlib library installed
- [Rust](https://rust-lang.org/) programming language with `cargo` and associated tools installed. 

#### Commands

```sh
git clone https://github.com/bluenote-1577/myloasm-kmc.git
cd myloasm-kmc
cargo install --path . # installs myloasm-kmc-v1 into ~/.cargo/bin

myloasm-kmc-v1 --help
```

`myloasm-kmc-v1` should be in your `PATH` after this. It must be in `PATH` for the `--kmc` option to work. 

