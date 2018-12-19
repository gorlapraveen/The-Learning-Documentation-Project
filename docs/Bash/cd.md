In Bash script, simple use of `cd` is useless. Because as script executes in same directory, it can't change its directory while executing.

Insted You can use `bash -c "cd some_directory && command"` to execute `command` in `some_directory`