## init project

    * 



## installation
* install rustup
* set up toolchain to nightly
* set up env variables:
    ```
    >rustup component add rust-src
    # stable
    export RUST_SRC_PATH=~/.multirust/toolchains/[your-toolchain]/lib/rustlib/src/rust/src
    # nightly
    export RUST_SRC_PATH="$HOME/.multirust/toolchains/nightly-x86_64-apple-darwin/lib/rustlib/src/rust/src"
    ```
* install clippy
* install rust vscode extensions
    * rust, better toml, LLDB

* [Setting up a Rust Development Environment](http://asquera.de/blog/2017-03-03/setting-up-a-rust-devenv/)
* [install RLS(rust language server)](https://github.com/rust-lang-nursery/rls)