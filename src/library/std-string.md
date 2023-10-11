# String processing

In Rust the string type these functions operate on is called `OrcString`. This is either a token for an interned string or an `Rc<String>` if the string was been programmatically constructed (eg. using the functions in this library).

All functions here operate on Unicode graphemes. This essentially means that letters with added diacritics and Mandarin multi-codepoint characters are treated as a single character. It also means that there isn't a "character" type, because a single character of zalgo text may be very large.

**size** `OrcString -> usize` <br/>
Finds the size of the text in bytes. This should be used to determine the computational resource utilization of strings. It should not be used to decide whether to truncate text.

**len** `OrcString -> usize` <br/>
Finds the number of graphemes in the text. This can be used for example to truncate text. It should not be used to limit the size of messages for security purposes.

**concat** `OrcString -> OrcString -> OrcString` <br/>
Appends a string to another. Also available as infix operator `++` which is available globally.

**slice** `OrcString -> usize -> usize -> OrcString` <br/>
Takes a string, a start and a length in graphemes. Slices out the specified subsection of the string.

**find** `OrcString -> OrcString -> Option usize` <br/>
If the first string contains the second then returns the index. See [std::option](std-option.md) for how to operate on the value.

**split** `OrcString -> usize -> tuple[OrcString, OrcString]` <br/>
Splits the string into two substrings at the nth grapheme. See [std::tuple](std-tuple.md) for how to operate on the value

**char_at**`OrcString -> usize -> OrcString` <br/>
Returns the nth grapheme.