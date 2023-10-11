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

If the item is a constant, the name and type are obvious and the example is optional. Types use the Haskell arrow `->` to indicate a function from one type to another. If the item is a macro system, the name is the name by which the macro should be referenced in free language, and the type is the category of the macro. The categories are as follows

- `operator`: binary operator
- `expression`: expression-like syntax, such as if/then/else
- `syntax`: anything that binds names (creates lambdas)
- `<type>(<dependencies>)`: custom syntax that gets triggered by other custom syntax, with a list of trigger tokens that should be referenced to understand when and how this macro is invoked. (`<type>` is `syntax` if either the dependency or this syntax binds names, `expression` if neither do)