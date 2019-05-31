


T:?sized: 
    * 大部分的类型基本上都是 Sized，就是编译期间大小就已经确定了，但是有个别类型大小是编译期间不能确定的，比如[]数组类型和str类型
        * We can only manipulate an instance of an unsized type via a pointer. An &[T] works fine, but a [T] does not.
        * Variables and arguments cannot have dynamically sized types.
        * Only the last field in a struct may have a dynamically sized type; the other fields must not. Enum variants must not have dynamically sized types as data.

never type: 
    * a type never return 
    * can be coerced to any other type
    * `continue, loop, panic` all return never type.