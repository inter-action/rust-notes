# cargo

* commands:

    cargo new hello_world --bin

* 两种dep形式

    [dependencies]
    glob = "0.2.11"
    log = "0.3.6"
    notify = "2.6.3"

    [dependencies.clap]
    version = "2.14"
    default-features = false
    features = ["wrap_help"]