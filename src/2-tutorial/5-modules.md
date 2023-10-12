# Modules and visibility.

Each folder and file is a module. In addition, submodules can be defined within files with the syntax `module <name> ( <lines> )`. Constants and submodules defined in a file are private by default and can be exported with the `export` prefix.

```orc
-- in tool.orc
module implementation (
  const hidden_data := "foo"
  export const some_operation := \s. s ++ hidden_data
)

export module public (
  import super::implementation

  export const do_stuff := implementation::some_operation
)
```

```orc
-- in main.orc
import tool::public::do_stuff

const main := do_stuff "bar"
```

`super` at the beginning of an import path points to the enclosing module, much like it does in Rust.