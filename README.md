<div align="center">
  <h1>sealevel-go 🌊</h1>
  <p>
    <strong>Go library embedding the Solana Sealevel runtime</strong>
  </p>
  <sub>Built with Go and 🦀 at <em>REDACTED</em></sub>
</div>

## Summary

This Go library allows you to execute Solana bytecode format programs without a blockchain node.

It interfaces with `libsealevel`, the C library wrapping `solana-bpf-program-loader` and `solana_rbpf`.

## How to build

sealevel-go is under heavy development. ️🦺

To run, you'll need to …

- build `libsealevel` from Solana sources;
- install headers and shared library to your path;

```shell

# install dependencies (maybe not needed?)
apt install gcc-multilib

# Check out `libsealevel`.
git clone https://github.com/terorie/libsealevel
cd libsealevel

# Build libsealevel
cargo build --release

# Install header
ln -s "$(pwd)/sealevel.h" /usr/local/include/sealevel.h

# Install library (Linux)
ln -s "$(pwd)/target/release/libsealevel.dylib" /usr/local/lib/libsealevel.dylib
# Install library (macOS)
ln -s "$(pwd)/target/release/libsealevel.so" /usr/local/lib/libsealevel.so

export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib

ld -lsealevel --verbose
# if you get "ld: warning: cannot find entry symbol _start," is good.
```

Then, simply Go build as usual.

```shell
go vet .
go build .

# install github large-file-storage (so you can fetch minimal.solana.so example program)
git lfs install
# fetch minimal.solana.so
git lfs checkout

# run tests
go test .
```
