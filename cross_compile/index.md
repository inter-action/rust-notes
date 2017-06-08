# cross compile

* use attribute: #[cfg(target_family = "windows")]

    impl Runner {
        #[cfg(target_family = "windows")]
        fn clear(&self) {
            let _ = Command::new("cls").status();
        }

        #[cfg(target_family = "unix")]
        fn clear(&self) {
            let _ = Command::new("clear").status();
        }

    }

* use macro

    let output = if cfg!(target_os = "windows") {
        Command::new("cmd")
                .args(&["/C", "echo hello"])
                .output()
                .expect("failed to execute process")
    } else {
        Command::new("sh")
                .arg("-c")
                .arg("echo hello")
                .output()
                .expect("failed to execute process")
    };