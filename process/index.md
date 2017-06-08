



* spawn & kill a command in unix

    #[cfg(target_family = "unix")]
    fn kill(child: &mut Child) {
        // declaration
        extern {
            // http://www.tutorialspoint.com/unix_system_calls/killpg.htm
            fn killpg(pgrp: libc::pid_t, sig: libc::c_int) -> libc::c_int;
        }

        // call
        // libc::SIGTERM, signal_terminate
        unsafe {
            killpg(child.id() as i32, libc::SIGTERM);
        }
    }


    // todo: update this
    // setpgid: http://man7.org/linux/man-pages/man2/setpgid.2.html
    #[cfg(target_family = "unix")]
    fn invoke(&self, cmd: &str, updated_paths: Vec<&str>) -> Option<Child> {
        use libc;

        let mut command = Command::new("sh");
        command.arg("-c").arg(cmd);

        if updated_paths.len() > 0 {
            command.env("WATCHEXEC_UPDATED_PATH", updated_paths[0]);
        }

        let child = command
            .spawn()
            .ok();

        if let &Some(ref c) = &child {
            unsafe {
                libc::setpgid(c.id() as i32, c.id() as i32);
            }
        }

        child
    }
