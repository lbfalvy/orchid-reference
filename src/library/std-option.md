# Option

```orc
option T = U -> (T -> U) -> U
```

An option either contains a value or contains nothing. It is represented as a function which takes two parameters. If the option is empty, it returns the first. If the option contains a value, the second parameter is applied as a function to the contained value.

## some

```orc
T -> option T
```

Wraps the value in an option

## none

The empty option.

## map

```orc
option T -> (T -> U) -> option U
```

Applies a function to the value in the option.

## flatten

```orc
option (option T) -> option T
```

## flatmap

```orc
option T -> (T -> option U) -> U
```

## unwrap

```orc
option T -> T
```

returns the value in the option, or panics if none is found