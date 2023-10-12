# Procedural

This library contains syntax constructs to break code into multiple statements and name bindings which can be read in a familiar top-down order.

**do{}** `expression` <br/>
a modular block that converts semicolon-delimited statements into a linked list of `statement` tokens, enabling both the standard library and external modules to define custom statements.

```orc
import std::to_usize

const main := do {
  let a = 5;
  cps b = readln;
  let c = to_usize b;
  c + a
}
```

**statement** `expression(do)` <br/>
It's possible to add support for custom statements by defining macros with a pattern of `statement ( <custom statement matcher> ) (...$next)` where `next` is an expression describing the rest of the block. This mechanism is used to define `std::loop::while` for example.

**let** `syntax(statement)` <br/>
`let` statements bind an expression to a name so it can be used in subsequent lines.

```orc
do {
  let a = 5 + 2;
  let b = (\x. x * x);
  b a
}
```

**cps** `syntax(statement)` <br/>
a statement to encapsulate a callback flow, passing control to another function. Most commonly used to allow the called function to execute impure operations.

```orc
const load_data := \callback. callback 10 20

const main := do {
  cps a, b = load_data;
  a + b
}
```

**do cps {}** `expression` <br/>
Allows to return a sequence of statements as a `cps` operation which can be called in other blocks. Most commonly used to put sequences of `cps` operations in the branches of a conditional.
