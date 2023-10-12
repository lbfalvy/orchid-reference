# Map

A map implemented as a list of key-value pairs. This isn't very efficient so it should only be used with relatively few keys.

These maps may be well-formed if each key appears exactly once, or degenerate if a key appears multiple times. Which one to use is up to the programmer. Well-formed maps are managed with `set` and `del`, while degenerate maps are managed with `add` and `delall`. A degenerate map may be turned into a well-formed map via `normalize` which is `O(n**2)`.

**empty** `map ? ?` <br/>
Creates a new empty map

**add** `map K V -> K -> V -> map K V` <br/>
Adds the element to the map, possibly shadowing an existing element with the same value

**get** `map K V -> K -> option V` <br/>
Returns the first value associated with this key if it exists

**del** `map K V -> K -> map K V` <br/>
Removes the first occurrence of a key.

**delall** `map K V -> K -> map K V` <br/>
Removes all occurrences of a key.

**set** `map K V -> K -> V -> map K V` <br/>
Replace at most one occurrence of a key with a new one.

**normalize** `map K V -> map K V` <br/>
ensure that there's only one instance of each key in the map.

**new[]** `expression` <br/>
Creates a new list from a comma-separated sequence of `key = value` pairs.

```
const foo := map::new[ "foo" = 1, "bar" = 2, "baz" = 3, "bar" = 4 ];
```
