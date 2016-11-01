# Beginning Workshop: Command Line Apps Part II 

# Spawning Processes
https://gobyexample.com/spawning-processes

# Exec'ing Processes
https://gobyexample.com/execing-processes

# Handling Signals
https://gobyexample.com/signals

## Exit and Exit Codes
When your program shuts down, users (sysadmins, etc) will expect it to behave like any other UNIX/Linux utility. Hence, you will want to exit cleanly and perform as expected when you application receives OS signals like SIGINT, SIGHUP and others.

Example: https://gobyexample.com/exit

Most Go applications can use `os.Exit(code int)` or something that implicitly calls on `os.Exit` like `log.Fatal`.

ProTip: Avoid using `os.Exit` or code that calls on `os.Exit` during unit tests. The test run will simply exit and short-circuit.