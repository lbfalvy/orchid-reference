# System::Async

Asynchrony in Orchid is realised via a central event loop that is available for all systems. As such, the tools used to control asynchrony are universal.

**yield** `cmd` <br/>
A standalone command. When returned as the value of a program, instructs the event queue to wait for the next event.

```
export const print := \text. \ok. (
  io::write_str io::stdout text
    (io::flush io::stdout
      ok
      (\e. panic "println threw on flush")
      \_. yield
    )
    (\e. panic "print threw on write")
    \_. yield
)
```

Orchid's IO is actually completely asynchronous; `write_str` and `flush` both take three callbacks, success, failure, and the sync next step. Since `print` blocks until the text is on the screen, after each of these commands we place the continuation in success and `yield` as the sync next step. If we wanted to do more work while our text gets printed, we could've used `write_str` directly and put the rest of the operation in its sync next step.

**set_timer** `bool -> number -> cmd -> (cmd -> cmd) -> cmd` <br/>
Sets a timer. Parameters specify whether the timer is recurring, the delay in seconds, the command to be executed when the timer fires, and the sync next step. The sync next step receives a canceller which is itself a command. If this command is called, later iterations of the timer will not run.

```
import system::async::(set_timer, yield)
import system::io::(readln, println)
import std::exit_status

const main := (
  set_timer true 1 (println "y" yield) \cancel.
    readln \a.
      cancel
        exit_status::success
)
```
