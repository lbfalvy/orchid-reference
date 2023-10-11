# Loop

Exposes a variety of macros related to recursive looping.

## loop_over

```orc
const factorial := \a. loop_over (a, b=1) {
  let b = b * a;
  let a = a - 1;
  cps if a == 1
    then return b
    else identity;
}
```

This macro accepts a list of loop variables which may be initialized inline as the example shows, and the body of a `do{}` block except for the final expression. Between iterations of the loop only the loop variables are retained. Remember that these are still not mutable variables, so updates to their values are still done with `let` bindings.

## while

```orc
const factorial := \i. do {
  while i > 0 (i, prod=1) {
    let prod = prod * i;
    let i = i - 1;
  };
  prod
}
```

This macro may only be used as a statement within `do{}` blocks, and accepts a boolean expression and the same loop variables and body as `loop_over`. While the former only keeps track of the loop variables within the loop body, here all loop variables keep their value for the rest of the block.

Note that bindings within the loop that aren't loop variables are not visible outside the loop, that `while` must be followed by a semicolon like other Orchid statements but unlike `while` loops in most procedural languages, and that the condition can reference loop variables initialized in the loop variable list despite appearing before them in the code.

## recursive

```orc
-- excerpt from std::list
export const map := \list. \f. (
  recursive r (list)
    pop list end \head. \tail.
      cons (f head) (r tail)
)
```

This macro is a relatively low-level wrapper for the Y-combinator which avoids some common pitfalls around manually emulating loop variables. It takes a name that the recursive callback will be bound to (convenitonally set to `r` if available), a variable list like the other loops, and captures all code up to the next closing paren as a body. Unlike the other loops, this one doesn't imply a `do{}` body and doesn't automatically forward values wherever `r` appears, instead, it's the user's responsibility to pass the correct number of arguments to `r`, one for each variable.

> **info**
> 
> Passing a different number of arguments to `r` than the number of loop variables generates either a function or a function call with a number of arguments specified at runtime, which is an unusual but legitimate use of the macro. A recursive expression which contains both a call with an extra argument and a call with too few arguments is computationally equivalent to a stack machine.

## Y

This constant is the basis for all other recursive structures, the Y-combinator. It takes a function `f` of type `T -> T` and returns `T` by calling `f (Y f)`. In an eager language this would be an infinite loop, but since Orchid is lazy it is completely safe so long as `f` defers the evaluation of its argument.