
* https://doc.rust-lang.org/book/first-edition/documentation.html

rustdoc tool can be run through cargo doc, one important feature is it can have embeded tests.

* syntax 
    * it starts with triple slash `///`, and it doc next thing to it. if not found , error will be throw
    * it use markdown syntax
    * `//!`, document the enclosing item, commonly modules, or crate documentation.
    
* sepecial sections
    * there four sepcial sections in rust right now, syntax ```/// #<section_name> ```
    * ``` /// #Panics|Errors|Safety|Examples```

* Documetation as test(embeded test in doc) 
    * rust can only run test as doc in lib target, not binary one, due to linking issue. 
    * by default, your embeded code would be automatically wrapped in ``` fn main(){} ``` code block, except
        * having used ```extern crate <name>```
        * testing macros
            ```
            ```
    * using `#` before lines in your embeded rust code will hidden the line from being printed in docs.

    * examples:
        ```
        /// ```rust,should_panic
        /// assert!(false);
        /// ```

        /// ```rust,no_run
        /// loop {
        ///     println!("Hello, world");
        /// }
        /// ```
        ```
* enforcing documentation
    ```
    #![warn(missing_docs)]
    #![deny(missing_docs)]
    #[allow(missing_docs)]
    #[doc(hidden)]
    ```