# lang:core_traits


### 类型转换: (Module core::convert)

* AsRef

    * `fn as_ref(&self) -> &T;` 
        * `pub fn from_file<P: AsRef<Path>>(path: P) -> Result<Config> {`
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

* Into & From:
    * Into & From 是对称的互补操作, 即 A Into B, From B -> A
    * From:
        用来实现从一个类型转换到另一个类型，主要的用途是在try macro的error处理上, try macro会自动将error转换成目标函数可以接受
        的error类型，内部的机制就是调用From trait的方法
        
        * FromStr, 从str中反向解析该类型
    
* FromStr:
    * convert string to a type.


### 生命周期

* Copy & Clone
    * copy 是bit-wise copy, 一般可以由rust自动实现只需要derive或者implement copy给对应的type
    * Clone 是 Copy 的 supertype， 意味着 implement copy 一定是可以 clone 的
    * Clone 是 overloadable ?
    * Clone 可以对不同类型提供不同的实现, 
    * clone 是需要调用 clone 方法手动触发，而copy是implicit的, x = y 就触发了y的copy


* Drop: 垃圾清理用的, rust在对象go out scope的时候回调用里边的方法

* std::borrow::ToOwned: 将一个引用的对象转换成 owned type. 和 clone 区别是, clone 是 &T->T 的转换, 而这个更加的generialize.
    
    ```
    pub trait ToOwned {
        type Owned: Borrow<Self>;               // Borrow<str>: T->&T
        fn to_owned(&self) -> Self::Owned;

        fn clone_into(&self, target: &mut Self::Owned) { ... }
    }

    let s: &str = "a";
    let ss: String = s.to_owned(); // s.to_owned() return a type Borrow<str>, String 对象实现了 Bowrrow<str>
    ```


### Others
* Eq & PartialEq
    * PartialEq: 用于比较两个值是否相等, 实现trait或者使用attribute。
    * Eq： 用于比较是否相等 x == y
    * 两者的差异？感觉没差异呀
        * pub trait Eq: PartialEq<Self>, 
        * 下面的链接有介绍, 说是Eq必须是reflective的, 即 for all x in set(x) assert x Relation x is true.

    * PartialEq 用的比较多，struct derive 的时候一般都用这个, 内部的fields都相等, 那这个 struct 就相等
* Hash:

* Debug & Display, ToString:
    * Debug: 用于打印debug信息, rust compiler会自动deserialize对应类型中的变量
    * Display: 主要用于println展示用的
    * ToString: 
        * to_string()->String
        * 实现了Display, ToString就自动被实现了

* core::default::Default, provide default values.

## Links
* [Rust's Built-in Traits, the When, How & Why](https://llogiq.github.io/2015/07/30/traits.html)