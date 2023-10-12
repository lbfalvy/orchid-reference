# Hello World

Orchid programs are made up of expressions, and the only effect expressions have is their value. The value of the whole program is printed by the interpreter. As such, the Hello World program in Orchid is as simple as:

```orc
-- in main.orc
const main := "Hello World!"
```

This should print `i"Hello World!"` on the terminal. The `i` stands for interned. Orchid strings can be interned and literals are interned by default. Equality comparison between interned strings is very fast. This optimization is a cornerstone of Javascript's performance.

Comment syntax is inspired by Lua; line comments start with `--` and stretch until the end of the line, while block comments start with `--[` and end with `]--`.

Constants are written as `const <name> := <expression>` terminated by a newline, and they allow you to extract subexpressions for brevity. If you add parentheses around an expression its meaning doesn't change, so long constants can be wrapped in parentheses and broken to multiple lines. The value of the program is the value of the constant `main`.

Other than line breaks ending semantic items when they appear outside parentheses, whitespace is never significant.