# Control flow

There are various convenient syntax structures in the standard library to make working with expressions more convenient. The most common of them is the `do` block, which enables us to bind names to subexpressions, and also presents a modular framework other modules can use to interact with control flow. What this means exactly will be shown in later sections.

Notice also that the last line in the `do` block is an expression. Every orchid expression must have a value, and the expression `do{}` desugars to is no exception.

```orc
const main := do {
  let foo = 12;
  let bar = foo * (foo - 1);
  to_string bar
}
```

Expressions are evaluated when their value is used, and there isn't any way to update the value bound to names, so the primary mechanism for looping is recursion. There are looping constructs in the standard library which abstract away the act of recursion so in practice the perogrammer rarely needs to consider this fact.

```orc
const main := do {
  let i = 5;
  while i > 0 (i, prod=1) {
    let prod = prod * i;
    let i = i - 1;
  };
  prod
}
```