# Option

```orc
option T = U -> (T -> U) -> U
```

An option either contains a value or contains nothing. It is represented as a function which takes two parameters. If the option is empty, it returns the first. If the option contains a value, the second parameter is applied as a function to the contained value.

**some** `T -> option T` <br/>
Wraps the value in an option

**none** `option ?` <br/>
The empty option.

**map** `option T -> (T -> U) -> option U` <br/>
Applies a function to the value in the option.

**flatten** `option (option T) -> option T` <br/>

**flatmap** `option T -> (T -> option U) -> U` <br/>

**unwrap** `option T -> T` <br/>
returns the value in the option, or panics if none is found