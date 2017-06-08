
# error handling

* error pattern

    #[derive(Debug)]
    pub enum Error {
        Glob(glob::PatternError),
        Io(io::Error),
    }


    impl From<glob::PatternError> for Error {
        fn from(error: glob::PatternError) -> Error {
            Error::Glob(error)
        }
    }

    impl From<io::Error> for Error {
        fn from(error: io::Error) -> Error {
            Error::Io(error)
        }
    }

