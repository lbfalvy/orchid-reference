# Getting started

In order to start experimenting with Orchid, clone the language:

```sh
git clone https://github.com/lbfalvy/orchid
```

This is a Rust project with both a library and a binary target. The interpreter exposes simple I/O operations. When you start the interpreter with `cargo run`, The entry point is always `main.orc` in the current directory. `/examples` contains some demo projects that you can refer to while experimenting, this is also a great place to put your own projects.

It is possible to install the interpreter system-wide by running `cargo build --release` and then adding `target/release/orcx` which is a standalone executable to `$PATH`, but because the language is still heavily experimental and bugfixes and major features are added regularly it is easier to work in the repo and update with a simple `git fetch && git pull`.