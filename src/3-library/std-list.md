# List

A linked list data structure.

**cons** `T -> list T -> list T` <br/>
Adds an element to the head of the list

**end** `list ?` <br/>
Empty list

**pop** `list T -> U -> (T -> list T -> U) -> U` <br/>
Takes a list, a default value and a callback. Returns the default value if the list is empty, otherwise passes the head and tail to the callback.

**fold** `list T -> U -> (U -> T -> U) -> U` <br/>
Fold each element into an accumulator using a callback. This evaluates the entire list.

**rfold** `list T -> U -> (U -> T -> U) -> U` <br/>
Fold each element into an accumulator in reverse order. This evaulates the entire list, and isn't tail recursive.

**reduce** `list T -> (T -> T -> T) -> option T` <br/>
Fold each element into a shared element. This evaluates the entire list.

**filter** `list T -> (T -> bool) -> list T` <br/>
Return a new list that contains only the elements from the input list for which the function returns true.

**map** `list T -> (T -> U) -> list U` <br/>
Transform each element of the list.

**skip** `list T -> usize -> list T` <br/>
Skip N elements from the list and return the tail.

**take** `list T -> usize -> list T` <br/>
Return `n` elements from the list and discard the rest.

**get** `list T -> usize -> option T` <br/>
Return the `n`th element from the list.

**enumerate** `list T -> list tuple[usize, T]` <br/>
Map every element to a pair of the index and the original element

**chain** `list (T -> T) -> T -> T` <br/>
Chains a list of functions in revverse, calling the head of the list on the return value of the next element when called on the element after it and so on. The last element in the list receives the second argument.

The main use case is to turn a list of CPS commands into a single CPS command which executes all of them in order.

**new[]** `expression` <br/>
Creates a new list from a comma-separated sequence of elements.

```orc
const my_list := list::new[1, 2, "foo", 3.14, 22 / 7]
```
