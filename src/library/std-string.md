# String processing

In Rust the string type these functions operate on is called `OrcString`. This is either a token for an interned string or an `Rc<String>` if the string was been programmatically constructed (eg. using the functions in this library).

All functions here operate on Unicode graphemes. This essentially means that letters with added diacritics and Mandarin multi-codepoint characters are treated as a single character. It also means that there isn't a "character" type, because a single character of zalgo text may be very large.

## size

```orc
OrcString -> usize
```

Finds the size of the text in bytes. This should be used to determine the computational resource utilization of strings. It should not be used to decide whether to truncate text.

## len

```orc
OrcString -> usize
```

Finds the number of graphemes in the text. This can be used for example to truncate text. It should not be used to limit the size of messages for security purposes.

## concat

```orc
OrcString -> OrcString -> OrcString
```

Appends a string to another. Also available as infix operator `++` which is available globally.

## slice

```orc
OrcString -> usize -> usize -> OrcString
```

Takes a string, a start and a length in graphemes. Slices out the specified subsection of the string.

## find

```orc
OrcString -> OrcString -> Option usize
```

If the first string contains the second then returns the index. See [std::option](std-option.md) for how to operate on the value.

## split

```orc
OrcString -> usize -> tuple[OrcString, OrcString]
```

Splits the string into two substrings at the nth grapheme. See [std::tuple](std-tuple.md) for how to operate on the value

## char_at

```orc
OrcString -> usize -> OrcString
```

Returns the nth grapheme.