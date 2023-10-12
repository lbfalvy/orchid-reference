# system::FS

File system access methods

## OsString

This library uses `OsString` to represent paths, which isn't necessarily valid Unicode.

**os_to_string** `OsString -> result OrcString OsString` <br/>
Validates that the argument is Unicode

**string_to_os** `OrcString -> OsString` <br/>
Converts to OsString

**os_print** `OsString -> OrcString` <br/>
Converts an OsString to an OrcString for printing, replacing unrepresentable bytes with placeholders.

**join_paths** `OsString -> OsString -> OsString` <br/>
Join a path and a subpath according to the platform's rules.

**pop_path** `OsString -> option ( tuple[OsString, OsString] )` <br/>
Remove the last segment from a path.

**cwd** `OsString` <br/>
The current working directory.

## file operations

These return the same `IoOperation` as [system::io](system-io.md)

### Files

**read_file** `OsString -> IoOperation (ReadHandle -> cmd)` <br/>
**write_file** `OsString -> IoOperation (WriteHandle -> cmd)` <br/>
**append_file** `OrcString -> IoOperation (WriteHandle -> cmd)` <br/>

### Directories

**read_dir** `OrcString - ioOperation (list [OsString, bool] -> cmd)` <br/>
Returns a list of names alongside flags indicating whether the given entry is a subdirectory.