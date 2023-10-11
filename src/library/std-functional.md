# Functional

Primitives and operators for functional programming style.

**identity** `T -> T` <br/>
Returns its argument without modification

**pass** `T -> (T -> U) -> U` <br/>
Calls its second argument on its first argument.

**pass2** `T -> U -> (T -> U -> V) -> V` <br/>
Calls its third argument on its first two arguments in unchanged order

**return** `T -> U -> T` <br/>
Discards its second argument and returns the first

**&dollar;** `operator` <br/>
An operator borrowed from Haskell; it wraps the following tokens in parentheses to avoid accumulating closing parens in deeply nested sequences

```
to_string $ to_uint 3.14
```

**|>** `operator` <br/>
An operator borrowed from Elixir; it passes the left hand side as the first argument of the function, pushing all subsequent arguments back.

```
list::new[1, 2, 3, 4]
  |> list::filter (\x. x % 2 == 0)
  |> list::map (\x. x * 2)
```


**() =>** `syntax` <br/>
An alternative spelling of a function which has a lower priority than `do{}` blocks and doesn't have to be parenthesized to appear in them. Because it binds a name it still has to be higher priority than `|>` which is a simple operator, but this can improve ergonomics for some use cases involving callbacks.

```
const square := (x) => x * x
const square_sum := (a, b) => square a + square b
const square_double := x => square_sum x x
-- the parens are optional for unary functions
```
