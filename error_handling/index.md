
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


* error_chain mod:
    * http://brson.github.io/2016/11/30/starting-with-error-chain
    * https://github.com/brson/error-chain
    * 很方便地能把两个error chain 起来， 这样在报错的时候能给更多的context, sample.rs 代码中的 recursion_limit，表示最大的error嵌套的层级数目    

## links
* http://blog.burntsushi.net/rust-error-handling/#standard-library-traits-used-for-error-handling
* How Rust Helps You Prevent Bugs - https://polyfloyd.net/post/how-rust-helps-you-prevent-bugs/
## related libs

