# Exit Status

Return values for programs that suppress the printing of the final value. Returning one of these signals an orderly exit from a program that handles its own I/O.

**success** `cmd` <br/>
Constant indicating that the program had successfully completed its task.

**failure** `cmd` <br/>
Constant indicating that a problem occurred. Causes exit code 1 to be emitted on Unix.

**is_success** `cmd -> bool` <br/>
Returns `true` for `success`, `false` for `failure`.