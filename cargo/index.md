# cargo

* commands:

    cargo new hello_world --bin


* 两种dep形式

    [dependencies]
    glob = "0.2.11"                     # global
    errors = { path = "../errors" }     # local, relative path


    [dependencies.clap]
    version = "2.14"
    default-features = false
    features = ["wrap_help"]