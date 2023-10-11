# Getting started

In order to start experimenting with Orchid, you need a Rust toolchain. Instructions on how to install Rust on your system are available at [www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install).

Once you have a stable Rust toolchain installed, you can clone the repository:

```sh
git clone https://github.com/lbfalvy/orchid
```

`/examples` contains some demo projects that you can refer to while experimenting, this is also a great place to put your own experiments. When you start the interpreter with `cargo run`, it starts from `main.orc` in the current directory.

It is possible to install the interpreter system-wide by running `cargo build --release` and then adding `target/release/orcx` which is a standalone executable to `$PATH`, but because the language is still in heavy development and bugfixes and major features are added regularly it is easier to work in the repo and update the interpreter with a simple `git fetch && git pull`.