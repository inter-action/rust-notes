# lang:core_traits

* Copy & Clone
    * copy 是bit-wise copy, 一般可以由rust自动实现只需要derive或者implement copy给对应的type
    * Clone 是 Copy 的 supertype， 意味着 implement copy 一定是可以 clone 的
    * Clone 是 overloadable ?
    * Clone 可以对不同类型提供不同的实现, 
    * clone 是需要调用 clone 方法手动触发，而copy是implicit的, x = y 就触发了y的copy


* AsRef

    * `fn as_ref(&self) -> &T;` 
    * 显式地调用转换
    * 与 Deref 不同的是，这个可以被实现多次（返回不同类型）


* Deref
    * `fn deref(&self) -> &Self::Target;`
    * deref 这个很重要 , rust 有个概念 'Deref coercions' 就是用来实现不同type之间的implicit coercion.


    lazy_static! {
        static ref INTERRUPT_TX: Mutex<Option<Sender<()>>> = Mutex::new(None);
    }

    fn create_channel() -> Receiver<()> {
        let mut guard = INTERRUPT_TX.lock().unwrap();
        if (*guard).is_some() {
            panic!("interrupt_handler::install() already called!");
        }

        let (tx, rx) = channel();
        (*guard) = Some(tx);

        rx
    }

* Drop: 垃圾清理用的, rust在对象go out scope的时候回调用里边的方法

* Debug & Display, ToString:
    * Debug: 用于打印debug信息, rust compiler会自动deserialize对应类型中的变量
    * Display: 主要用于println展示用的
    * ToString: 
        * to_string()->String
        * 实现了Display, ToString就自动被实现了

* PartialEq: 用于比较两个值是否相等, 实现trait或者使用attribute。