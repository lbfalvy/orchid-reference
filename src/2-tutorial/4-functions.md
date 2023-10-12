# Functions

Function calls in orchid are the most fundamental step and do not use an operator. Functions are applied to arguments by simply writing the arguments after the function name.

```orc
import std::to_string

const main := to_string 3.14
-- prints r"3.14"
```

The "r" in the result of the above program indicates that the string is not interned.

Functions are first-class values, so the equivalent of defining a function in a procedural language is simply to assign a constant. Functions are written as "`\` argname `.` body"

```orc
const square := \x. x * x
const main := square 5
-- prints 25
```

All functions take a single argument, multi-parameter functions are represented by returning a function. This is called currying. The technique is most well known from Haskell.

```orc
const add_sqrs := \a. \b. a * a + b * b
const main := add_sqrs 3 5
-- prints 34
```

This also means that all parameters don't have to be provided at the same time. It's possible to store functions with some arguments missing.

```orc
const linear := \a. \b. \x. a * x + b
const scale2add3 := linear 2 3
const main := scale2add3 5
-- prints 13
```

We advise against doing this in most cases however as changes to the argument set may have unexpectedly deep architectural implications.

When the result of a function call is passed as the argument of another, the nested function call must be wrapped in parentheses:

```orc
import std::to_string

const sqr := \a. a * a
const main := to_string (sqr 5)
-- prints r"25"
```

Without the parens, this would attempt to stringify `sqr` and then pass 5 to the resulting string as though it was a function.