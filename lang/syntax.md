
* T:?sized 
    * https://doc.rust-lang.org/book/unsized-types.html
    * 大部分的类型基本上都是 Sized，就是编译期间大小就已经确定了，但是有个别类型大小是编译期间不能确定的，比如[]数组类型和str类型
        * We can only manipulate an instance of an unsized type via a pointer. An &[T] works fine, but a [T] does not.
        * Variables and arguments cannot have dynamically sized types.
        * Only the last field in a struct may have a dynamically sized type; the other fields must not. Enum variants must not have dynamically sized types as data.
    * 
    


* array vs slice
* two string type
* choose your own garentee

* trait:
    https://blog.rust-lang.org/2015/05/11/traits.html

    * as interface
    * Trait object as Dynamic dispatch
        * In Rust, a type like &ClickCallback or Box<ClickCallback> is called a “trait object”, and includes a pointer to an instance of a type T implementing ClickCallback, and a vtable: a pointer to T’s implementation of each method in the trait (here, just on_click)

    * static dispatch

    * [DST, Take 5](http://smallcultfollowing.com/babysteps/blog/2014/01/05/dst-take-5/), 
        * why trait is unsized: because trait is not the actual type, object's object type is unknow to the compiler
        * fat pointer:
            * [T]: array without knowning its with, it consists of (actual pointer, length of the array)
            * &T: trait object, it consists of (acutal pointer, v table of containing methods)
        
        

* closure:
    * ！！ http://huonw.github.io/blog/2015/05/finding-closure-in-rust/
    * rust 内部是用动态创建一个struct, 然后将所有需要包括在closure的变量声明在struct内部, 这个struct需要继承Fn, FnOnce, FnMut这些trait, 在这些trait内部实现对应的方法
    * 在这个struct中需要包括的变量到底是 reference(&), mutable reference(&mut), move. 编译器会根据closure的引用变量的方式来判断，来选择最灵活的。比如 closure 只有一个 `x+y` 代码， 那么 x y 都是 reference, 如果后面有 *x=3, 那么x将是 mutable reference. 如果需要将 closure 返回, 则一般需要 move 关键字, move会将所有的变量以move的形式定义struct
    * 由于trait（Fn, FnOnce, FnMut）是unsized, 所以不能在rust中传递, 只能用box封装, 或者使用trait object, 及&trait or Box<trait>, to make it pointer type.
    * 




## links

[rust attributes refs](https://doc.rust-lang.org/reference/attributes.html)