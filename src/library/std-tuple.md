# Tuple

Tuples are a primitive datatype. Together with [std::option](std-option.md), it can build any datastructure.

Tuples are constructed with a macro and consumed by a single function which reads out a field. To read data from a tuple you need to know its full length.

```orc
const numbers := t[1, 2, 3]
const main := pick numbers 1 3
-- evaluates to 2
```

## pick

```orc
tuple -> number -> number -> ?
```

Given a 0-based index and the total number of fields, returns the value of the requested field.
