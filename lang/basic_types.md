* Primitive Type pointer(Raw, unsafe pointers,):
    ！这个类型是分重要，必须要理解， 格式就是 *const T, *mut T
    https://doc.rust-lang.org/beta/std/primitive.pointer.html
    https://doc.rust-lang.org/book/raw-pointers.html#raw-pointers
    
    * 主要用于跟c代码进行交互
    * 没有rust生命周期的check, 这意味着你可以脱离rust生命周期的束缚，编译器不会check对应pointer的生命周期。
        * 没有自动的垃圾回收
        * rust compiler 不会保证对应的pointer的资源竞争的问题, (多线程环境下亦是如此)，这意味着数据可能出现脏读
        * 不会保证指针背后的数据为 non-null


* usize: usize 是根据机器的架构的类型变化的usigned integer类型, 代表了指针的大小。具体可以看链接:
    * https://stackoverflow.com/questions/29592256/whats-the-difference-between-usize-and-u32

* array

    ```rust
    let data = [1u8, 2, 3, 4, 5];
    ```