# Standard Library

These pages describe the Orchid modules included with the interpreter. Libraries under `std::` are fairly universal, but all of this may vary from environment to environment, possibly in subtle ways. For example, embedders may choose to reimplement part of the standard library in Rust for improved performance which the stock standalone interpreter defines in Orchid.

## Conventions in the library

Items are defined in the following format

---

**name** `type` <br/>
description

```
example
```

further notes if needed

---

If the item is a constant, the name and type are obvious and the example is optional. Types use the Haskell arrow `->` to indicate a function from one type to another, and capital letters to indicate generics. If the item is a macro system, the name is the name by which the macro should be referenced in free language, and the type is the category of the macro. The categories are as follows

- `operator`: binary operator
- `expression`: expression-like syntax, such as if/then/else
- `syntax`: anything that binds names (creates lambdas)
- `<type>(<dependencies>)`: custom syntax that gets triggered by other custom syntax, with a list of trigger tokens that should be referenced to understand when and how this macro is invoked. (`<type>` is `syntax` if either the dependency or this syntax binds names, `expression` if neither do)

In some places the types contain a primitive type `cmd`, this refers to an effectful command addressed to the interpreter or the environment. If the end result of a top level expression isn't a `cmd`, it gets printed and the interpreter halts. A very common pattern is `cmd -> cmd` at the end of a type, this simply means that the last argument to the operation is the next operation to execute. `(T -> cmd) -> cmd` (or `(T -> U -> cmd) -> cmd`) usually means that the operation produces some value (or values) which are available to the program when defining the next operation.