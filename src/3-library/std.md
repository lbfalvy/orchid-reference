# STD

These are constants defined directly under `std`, typically due to their special significance or fundamental nature.

**inspect** `T -> T` <br/>
Debug-logs its argument then returns it without normalization.

**panic** `OrcString -> nothing` <br/>
Prints an error with a customizable error message, then halts. This expression never returns, so it can be used to mark dead code paths.

**known::,** `token` <br/>
The sole purpose of this export is to ensure that this token has the same namespaced name across files in usercode. `,` is an intrinsic operator in Orchid but without an import it would just be a local name in each module, however needing to import it would lead to confusion as it's also used in the import statement.

## conv

Functions for converting types. All of these act as identity when passed their output type.

**to_float** `usize|float|OrcString -> float` <br/>
Converts a `usize` or `OrcString` to a `float`.

**to_uint** `usize|float|OrcString -> usize` <br/>
Converts a `float` or `OrcString` to a `usize`.

**to_string** `usize|float|bool|OrcString -> OrcString` <br/>
Converts a `float`, `usize` or `bool` to an `OrcString`
