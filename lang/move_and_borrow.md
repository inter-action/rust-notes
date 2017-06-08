
* `move ` keyword: 将变量move到closure中,这个在syntax.md中有描述

* `* <t:&i32>`  会将t转换成i32
* 

    ```rust
    let mut x = 3;
    let y = &mut x;
    let z = &*y;//引用到x, 从新创建个引用(reference)
    ```
* 
    ```
    let mut x = 32;
    let y = &mut x; //create a reference, aka. pointer type
    *y = 4; //change x = 4, * dereference reference.
    ```
