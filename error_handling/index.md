
# error handling

rust 中 error handling一直是一个比较复杂的主题, 不管是那个语言, 其实错误处理都是最麻烦的部分. 只不过其他的语言对错误的处理的机制太过简单, 而隐藏了问题的复杂性. 而rust提供了很robust的错误处理机制供你去选择.

error handling 个人还是推荐直接用 `error-chain` 这个库来做, 这种方式比较成熟, 其他都太naive了. 不过还是具体看场景.

语言中错误处理你需要面临的抉择

* 程序要不要立即挂掉 (yes-> panic)
* 如果是可恢复的错误, 你需要返回对应的错误类型, 供caller去处理
    * 需不需要堆栈信息
    * 需不需要caller对错误类型做识别


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


* error_chain 模块:
    * https://github.com/CrazyFork/error-chain, 我在自己的仓库有解释

## links
* http://blog.burntsushi.net/rust-error-handling/#standard-library-traits-used-for-error-handling
* How Rust Helps You Prevent Bugs - https://polyfloyd.net/post/how-rust-helps-you-prevent-bugs/
## related libs

