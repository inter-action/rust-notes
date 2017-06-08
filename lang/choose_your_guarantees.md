

[choose your guarantees](http://rust-lang.github.io/book/first-edition/choosing-your-guarantees.html#synchronous-types)

这里的工具是帮助你escape掉rust默认的Lifetime规则 


* Basic Pointer type

    * Box<T>
        * 分配在heap上

    * &T, &mut T, 编译期会检查的锁

    * `* const T` and `*mut T`
        * These are C-like raw pointers with no lifetime or ownership attached to them. 
        * 到底是怎么用的？

    * Rc<T>, Reference Counter:
        * 运行时动态检查, 有运行时的overhead
        * 主要作用就是允许多个变量 owning 底层的包装的数据，当所有的变量都go out scope，才会触发清理机制
        * 非线程安全

    * Weak<T>
        * This is a non-owning, but also non-borrowed, smart pointer. It is also similar to &T, but it is not restricted in lifetime—a Weak<T> can be held on to forever. However, it is possible that an attempt to access the inner data may fail and return None, since this can outlive the owned Rcs. This is useful for cyclic data structures and other things.



* Cell type:

    * overview:
        * Cells provide interior mutability. In other words, they contain data which can be manipulated even if the type cannot be obtained in a mutable form (for example, when it is behind an &-ptr or Rc<T>).

    * Cell<T>:
        * 这货的主要作用就是enable多个mutable reference. 然后调用set方法改变内部的对象的值, 最后一次改变生效

    * RefCell<T>:
        * 主要通过 `borrow` 和 `borrow_mut` 方法来在运行时保证变量的锁。如果代码在运行时违反了规则，程序直接回panic掉
        * enable 多个变量引用底层的对象
        * 有运行时的overhead

    * UnsafeCell<T>:
        * is a cell type that can be used to hold any data and has no runtime cost, but accessing it requires unsafe blocks


* Synchronous types: 线程同步类型

    * Arc<T>: 
        * 和 Rc<T> 一样，它保证了所有线程的变量go out scope之后，销毁代码会运行

    * Mutex<T> and RwLock<T>:
        * Mutex<T> 和 RwLock<T> 都会在 lock 的时候挂起当前线程，直到可以获得锁
        * 与 Mutex<T> 不同的是 RwLock<T> 可以允许持有多个read变量, 而当需要修改的时候只允许一个write变量





