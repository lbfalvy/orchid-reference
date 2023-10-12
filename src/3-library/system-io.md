# System::IO

IO primitives to work with streams. Streams can be defined by the environment or returned by external libraries.

The following definitions mention types `ReadHandle`, `WriteHandle` and `Error`. `ReadHandle` and `WriteHandle` are created externally. `Error` is meant to be an Orchid representation of Rust's `std::io::Error`, but for the time being it's just the integer `0`.

**print** `OrcString -> cmd -> cmd` <br/>
Writes the string to stdout, flushes, and continues once both operations completed.

**println** `OrcString -> cmd -> cmd` <br/>
Writes the string with a newline to stdout and flushes.

**readln** `(OrcString -> cmd) -> cmd` <br/>
Reads a line from stdin.

## Standard streams

Standard unix I/O streams

**stdin** `ReadHandle` <br/>
**stdout** `WriteHandle` <br/>
**stderr** `WriteHandle` <br/>

## I/O operations
An IO operation `IoOperation T` has the type `T -> (Error -> cmd) -> cmd -> cmd`. It is a command that takes an eventual success and error handler, and a continuation. The continuation does not wait for the current operation to complete. Operations on the same `ReadHandle` or `WriteHandle` are sequenced, but there are no ordering guarantees, so eg. if you want to write to a `WriteHandle` and then flush it, the `flush` call must appear in the success path and not the continuation.

**read_string** `ReadHandle -> IoOperation (OrcString -> cmd)` <br/>
Reads the entire stream to a string.

**read_line** `ReadHandle -> IoOperation (OrcString -> cmd)` <br/>
Reads the stream up to the next line break, consuming the line break and returning all text before it.

**read_bin** `ReadHandle -> IoOperation (Binary -> cmd)` <br/>
Reads the entire stream into a blob as defined in `std::binary`.

**read_n_bytes** `ReadHandle -> usize -> IoOperation (Binary -> cmd)` <br/>
Reads N bytes from the stream and returns them in a blob. Remember that bytes don't translate to Unicode characters.

**read_until** `ReadHandle -> usize -> IoOperation (Binary -> cmd)` <br/>
Accepts a byte value no greater than 255. Reads the stream until the specified byte is found.

**write_str** `WriteHandle -> OrcString -> IoOperation cmd` <br/>
Writes the given string to the stream.

**write_bin** `WriteHandle -> Binary -> IoOperation cmd` <br/>
Writes the given bytes to the stream.

**flush** `WriteHandle -> IoOperation cmd` <br/>
Signals for any buffered data in the stream to be flushed. If you're writing to standard output explicitly instead of using `print`, you need to call this manually.

