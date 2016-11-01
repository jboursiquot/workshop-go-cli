# Beginning Workshop: Command Line Apps Part I

## Before we begin
* Set your `$GOPATH` and ensure your system is aware of it (`echo $GOPATH` should not return blank)
*  Ensure your `$GOPATH` is in your `$PATH` so it can be found outside of your project folder

## Package main and the main func
* Go applications produce a single executable.
* The `package main` is the only required package for any Go program.
* A `main` function is required as the entry point into the Go program.
* You cannot `import` anything from the `main` package, meaning any code you put into `package main` is not available for import to other go programs.

Example program: https://gobyexample.com/hello-world

**ProTip**: Separate the logic of what your package provides as functionality from the interface that allows one to use it--in this case, the CLI.
(Show example)

### Exercise
We're going to be building a program that outputs proverbs, specifically, the Go Proverbs (https://go-proverbs.github.io).
Let's start off real easy. Write a go program that prints out all the Go Proverbs on the terminal screen and meets the following requirements:

* Ensure your program can be built using `go build`
* Ensure your program is installable with `go install`
* Ensure you can locate your built program in the `$GOPATH`
* Ensure you can run your program from anywhere on your system

## Command Line Arguments
CLI arguments help you parameterize your programs. Head over to https://gobyexample.com/command-line-arguments.

### Exercise
It's time to extend your program by allowing it to take a numeric argument indicating which proverb to display (e.g. `proverbs 5`). It should meet the following requirements:

* Takes a numeric argument and display a single proverb matching the position of that proverb in the list. Note that your list can (should be) 0-based.
* Non-numeric arguments should be rejected
* Non-positive arguments can be converted to their absolute counterparts
* Arguments that go beyond the bounds of the list of proverbs should be rejects (e.g. asking for the 45th proverb when there are only 19 should rebuke the user).

ProTip: There's the hard way to do this (manipulating a string blob to extract text at the right position) and there's the easy way involving slices (https://gobyexample.com/slices). 

## Command Line Flags
Flags are commonly used for CLI-based applications when there's a need to specify options (e.g. `ls -l` where the `-l` flag tells the program to alter the output you would have gotten otherwise). See https://gobyexample.com/command-line-flags for how to extract flags in your program.

### Exercise
Continuing to build on our `proverbs` program, let's refactor our program to take `-f` flag and a value indicating a string to search our list of proverbs. If found, the proverb(s) are listed.

For example, `proverbs -f cgo` should find the two `cgo` references and return:

```
Cgo must always be guarded with build tags.
Cgo is not Go.
```

Requirements:
* Search should be case-insensitive
* Nothing is returned when there's no match

## Environment Variables
When you need your application to behave differently depending on its environment, you use environment variables. See https://gobyexample.com/environment-variables. `os.Getenv` is used to retrieve values from the environment while `os.Setenv` is very useful for setting/overriding those variables (especially during testing).

### Exercise
Add a new command to your program that, when triggered, lists all environment variables found.

## Reading Files
It's quite common to want to read files from disk during the execution of your programs. Using https://gobyexample.com/reading-files as your reference, we're going to make our `proverbs` program a bit more flexible by allowing it to load its list of proverbs from the file system rather than baking them into the program.

### Exercise
Extend your program by allowing it to take a check the environment for a `PROVERBS_FILE` environment variable. If found, `PROVERBS_FILE` will contain the path to file containing a list of proverbs to be read into memory. 

Your program should then be able to perform the same functions as it did before (e.g. listing, searching, showing a specific proverb).

You can either `export` your environment variable in the shell in which you build and execute your program or you can specify the variable at invocation time like so:

```bash
$ PROVERBS_FILE=/some/path/to/proverbs.txt proverbs -f cgo
```

## Writing files
It is just as common a practice to write files to disk from your programs as it is to read them. Next up, we are to extend our program to write the proverbs that are listed, shown or found to a file. You may use https://gobyexample.com/writing-files as a reference for how to write files to disk.

### Exercise
Extend your `proverbs` program so it can take a `-o` flag whose arguments is the path to which the results of your operation should be written. 

For example: `proverbs list -o my-proverbs.txt` should output the contents that would have been written to `STDOUT` into `my-proverbs.txt` instead.

Note that the same behavior is expected from all the commands and flags you've been supporting so far. The only difference is that you have have an option to write the output to disk.