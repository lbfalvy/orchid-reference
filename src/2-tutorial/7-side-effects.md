# Side Effects

Orchid is a pure functional language, so side effects cannot arise from the evaluation of functions. Instead, some functions return commands which can be executed by returning them as the value of the entire program. Of course, this way a program could only do one thing, so the commands also store the rest of the program; an expression to evaluate after the command has exacted its effect.

```orc
import system::io::*
import std::exit_status

const main := (
  print "Hello, user! what is your name?" (
    readln \name.
      println ("Goodbye, " ++ name ++ "!") (
        exit_status::success
      )
  )
)
```

In the above example, `print` and `println` take a third argument which is evaluated after the text is printed, and `readln`'s argument is a callback which is passed the newly read string. The values of all of these are treated the same as the value of the main program itself, forming a linked list of commands. This method of defining operations is called continuation passing style.

`std::exit_code::success` is simply a custom constant that isn't printed by the interpreter. Since all Orchid programs must have a value, `println` must take a third argument and any other value would be debug-printed by the interpreter. `std::exit_code::failure` does the same thing except it causes the interpreter to exit with code `1`.

## cps

Ideally we would like to avoid writing code like the above example, which is reminiscent of early Node.JS APIs commonly referred to as callback hell. To address this, `do` blocks support a statement type prefixed with `cps`, shorthand for continuation-passing style.

`let <name> = <expression>; <rest of block>` approximately desugars to `(\<name>.  <rest of block>) (<expression>)`. This binds the value to the name in the context of the rest of the block. In contrast, `cps` passes the rest of the block to the expression, where it is assumed to fill the place of the continuation in an effectful command. This statement can bind not just one but zero or multiple names, corresponding to the number of arguments passed to the continuation by the expression.

```orc
import system::io::*
import std::exit_status

const main := do {
  cps print "Hello, user! what is your name? ";
  cps name = readln;
  cps println ("Goodbye, " ++ name ++ "!");
  exit_status::success
}
```

Given how fundamental `cps` is, it can be combined with a lot of utilities from `std::cunctional`. For example, `cps foo = pass 1;` will assign 1 to `foo` and continue the program directly. `cps foo, bar = pass2 1 2;` does the same thing for two values. `cps identity;` is a no-op, and `cps return 2;` sets the value of the whole enclosing block to 2, discarding the following statements.

These primitves are most useful in situations like branching. If an if/then/else expression picks between commands, it must be called with cps, but this means that both branches must accept a continuation. If one branch is pure and the other is effectful, wrapping the pure branch in `pass`, `pass2` or `identity` can easily transform it to cps. `return` is useful as a break statement in some of the control structures exposed in [std::loop](../3-library/std-loop.md)

The final barrier to unbounded composition is `do` itself; although we can mix CPS and parametric statements within a block, the block itself still resolves to a single value, so injecting a `do` block containing CPS operations in another is not possible, since the continuation of the outer block is passed to the first command of the inner block. If we imagine a simplistic operation sequence `(op1 (op2 (op3)))`, then putting this in a `cps` statement followed by `op4` would produce `(op1 (op2 (op3)) op4)` and not `(op1 (op2 (op3 (op4))))`. This is really bad, `op1` doesn't even accept two arguments! To fix this, we introduce another block format `do cps { <statements> }` which desugars to `\cont. do { <statements> ; cont }`. This is itself a valid `cps` statement, so it can safely be returned in branches of `cps` expressions. Note also that, unlike a `do` block, a `do cps` block doesn't end in an expression.

```orc
import system::io::*
import std::exit_status

const main := do {
  cps print "access: ";
  cps name = readln;
  cps if name == "user"
    then println "welcome, uwer!"
    else if name == "admin"
    then do cps {
      cps print "password: ";
      cps password = readln;
      cps if password == "Passw0rd!"
        then println "welcome, admin!"
        else identity
    }
    else identity;
  exit_status::success
}
```
