# Beginning Workshop: Command Line Apps Part II 

# Spawning Processes
In this section, we'll use the common `grep` search utility on your (UNIX-like) OS to do the searching for you when your program is called with the previously added `-f` flag.

Your task is to "shell out" the search string to the `grep` utility to do the search rather than rely on your own string-searching logic.

Use https://gobyexample.com/spawning-processes as a guide for this exercise.

# Exec'ing Processes
https://gobyexample.com/execing-processes

# Handling Signals
https://gobyexample.com/signals

## Exit and Exit Codes
When your program shuts down, users (sysadmins, etc) will expect it to behave like any other UNIX/Linux utility. Hence, you will want to exit cleanly and perform as expected when you application receives OS signals like SIGINT, SIGHUP and others.

Example: https://gobyexample.com/exit

Most Go applications can use `os.Exit(code int)` or something that implicitly calls on `os.Exit` like `log.Fatal`.

ProTip: Avoid using `os.Exit` or code that calls on `os.Exit` during unit tests. The test run will simply exit and short-circuit.
