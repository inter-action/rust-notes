# advanced traits
* https://doc.rust-lang.org/book/ch19-03-advanced-traits.html#advanced-traits



## associated types & associated functions

associated types: 用来省略类型的, 如果你实现了某个trait.要不然每次使用都要指定泛型的类型, 如果用泛型去实现的话.


```rust
pub trait Iterator {
    // Item is a associated type on Iterator
    type Item;

    fn next(&mut self) -> Option<Self::Item>;
}
```

associated functions: 不接受 self 参数的函数, 说白了就是用来归类function的.

```rust
struct Dog;

impl Dog {
    // baby_name is an associated function, 
    fn baby_name() -> String {
        String::from("Spot")
    }
}
```

## orphan rule
Orphan rule: 
> we mentioned the orphan rule that states we’re allowed to implement a trait on a type as long as either the trait or the type are local to our crate. It’s possible to get around this restriction using the newtype pattern, which involves creating a new type in a tuple struct. 

这个规则的意思你只允许对某个type去实现trait, 前提是至少trait或者type一个在你的local scope中.

new type 和 DeRef 的组合去绕过这个限制, 还蛮有意思的.
