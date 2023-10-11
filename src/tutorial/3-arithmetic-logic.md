# Arithmetic and Logic

## Numbers

Basic arithmetic follows C-style syntax with infix operators and operator precedence:

```orc
const main := 2 + 2 * (3 + 4)
```

Orchid internally uses two number types; nonnegative platform-size integers represented with Rust's `usize`, and 64-bit floating point numbers that can never be `NaN`.

Number literals may be expressed in decimal, hex with `0x`, binary with `0b` and octal with `0o` prefix. Each of these may contain a decimal point and/or a decimal exponent separated by a letter `p` representing a power of the base. For example, `0xF.Fp11` means `0xFF00_0000_0000`. Number constants may contain underscores anywhere after the radix prefix for readability.

A number constant describes an integer if it doesn't have a decimal point and either doesn't have an exponent or the exponent is positive and not too large for a valid platform integer.

Multiplying, summing and taking module of integers results in an integer, all other operations return a float, which can be floored and cast to an `usize` with `std::to_uint`, like so:

```orc
import std::to_uint

const main := to_uint 4.5
```

## Booleans

Branching is done with the ternary operator if/then/else, which also has a return value:

```orc
const a := 2
const b := 3
const main := if a < b then b else a
```

The standard infix relational operators `==`, `!=`, `<`, `>`, `<=`, `>=` work on numbers. The infix operators `and`, `or`, and the function `not` can be used to combine booleans.

## Strings

Strings are enclosed in double quotes, support line breaks and common escape sequences. In addition, an escaped line break and the subsequent indentation are ignored:

```orc
-- prints i"foo and bar"
const main := "foo and \
               bar"
```

Strings support a variety of methods described in [std::string](../library/std-string.md)

numbers can be stringified with `std::to_string`, strings can be parsed to numbers via `std::to_uint` or `std::to_float` respectively. All three functions accept their return type and pass it through