

* 调用 system_call


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
