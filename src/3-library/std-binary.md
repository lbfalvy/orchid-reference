# Binary

These functions work with binaries, represented as a sequence of bytes.

**concat** `binary -> binary -> binary` <br/>
Appends a binary blob to another

**slice** `binary -> usize -> usize -> binary` <br/>
Copies out a subsection of the binary into a new blob specified by starting point and length

**find** `binary -> binary -> option usize` <br/>
Return the index where the second binary appears as a subsection of the first

**split** `binary -> usize -> tuple[binary, binary]` <br/>
Splits the binary into two halves at the given byte index

**int_bytes** `usize` <br/>
The length of a `usize` in bytes.

**get_num** `binary -> usize -> usize -> bool -> usize` <br/>
Takes a binary, a starting point, a length no greater than int_bytes, and a boolean indicating whether the encoding is little endian or not. Reads a `usize` from the specified location in the binary.

**from_num** `usize -> bool -> usize -> binary` <br/>
Takes a length no greater than int_bytes, a little endian flag and a number to encode. Turns the least significant _length_ bytes of the given `usize` in the specified endianness into a binary.

**size** `binary -> usize` <br/>
Returns the number of bytes in a binary
