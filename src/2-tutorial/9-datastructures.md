# Datastructures

The STL provides a few datastructures to accelerate work. These are mostly described in their respective library docs, [std::option](../3-library/std-option.md), [std::list](../3-library/std-list.md) and [std::map](../3-library/std-map.md). This page serves mostly to demonstrate how they can be used.

Most of these functions take the datastructure as the first argument, which makes it possible to chain them with `|>`.

```orc
import std::to_string

const fizz_buzz := n => (
  (recursive r (i=0) list::cons i $ r (i + 1))
    |> list::map (i =>
      if i % 15 == 0 then "FizzBuzz"
      else if i % 3 == 0 then "Fizz"
      else if i % 5 == 0 then "Buzz"
      else to_string i
    )
    |> list::take n
    |> list::reduce ((l, r) => l ++ "\n" ++ r)
    |> option::unwrap
)

const main := fizz_buzz 100
```
