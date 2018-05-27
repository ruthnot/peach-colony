+++
title =  "Chapter 2. Getting Started"
+++

### 2.1 Scripting Languages Versus Compiled Languages
* Most larger scale programs are written in a compiled language, such as Fortran, Ada, Pascal, C, C++ or Java.
* Compiled language are efficient, but usually work at a low level.
* Scripting languages are: Shell, Python, Perl, Ruby
* The advantage of scripting languages is that they are often higher level, being able to deal with objects such as
files and directories more easily.
* The disadvantage of scripting language is that they are less efficient.

### 2.3 A Simple Script

**$ who**

* shows know how many users are currently logged in

**$ who | wc -l**

* wc: word count, counts lines, words, and characters.
* wc -l: count just lines
* |: pipe symbol creates a pipe between two programs. who's output becomes wc's input

**$ cat > nusers**: create the file, and copy terminal input with cat (short for concatenate)

**who | wc -l**: type in desired command

**^D**: Ctrl-D is end of file

**$ chmod +x nusers**: Make it executable

**$ ./nusers**: Execute the script

### 2.4 Self-Contained Scripts: The #! First Line

* When runs a program, kernel will start a new process and run that program in that process. Kernal knows how to
do that automatically for a compiled program, yet don't know how for a script.

* That's why we use **#!** to tells the Kernal which interpreter to invoke.

* Most common one is #! /bin/sh - (the bare option says that there are no more shell options)

### 2.5 Basic Shell Constructs
* **;** semicolons seperate multiple command, shell will executes them sequentially
* **&** ampersand runs the command in the background
* **$** symbol is used to retrieve a variable value:
    *  **$ myvar=foobar ; echo $myvar**. Notice when assign the value, there can't be space near the = sign
    * **$ first=isaac middle=bashevis last=singer** multiple assignments are allowed on one line
    * **$ fullname="isaac bashevis signer" ; echo $fullname** use quotes if you want to assign value with spaces

##### printf
The full syntax of the printf command has two parts:

* The first is a string describing the desired output, second part is an argument list, such as a list of strings or
variable values: ***$ printf "The first program always prints '%s, %s!'\n" Hello world*** and it will output: The first
program always prints 'Hello, world!'
* **%** is the format specifier, two of the main format specifiers are **%s** for strings and **%d** for decimal integers
* **\n** is the escape sequence

##### Basic I/O Redirection
Standard I/O is perhaps the most fundamental concept in the Software Tools philosophy.
The idea is that programs should have a data source, a data sink (where data
goes), and a place to report problems. These are referred to by the names standard
input, standard output, and standard error, respectively.

* Change standard input with "<":   **$ tr -d '\r' < dos-file.txt**
* Change standard output with ">":   **$ tr -d '\r' < dos-file.txt > unix-file.txt**
* Think of < and > as data "funnels", data goes in to the big end and comes out of the small end

##### Special files: /dev/null and /dev/tty

* **/dev/null**: data sent to this file is thrown away by the system:
* **/dev/tty**: to get data typed by a human. (tty stands for teletypewriter)

##### Basic Command Searching

* **$PATH** is the search path of the system. It contains multiple bin directory
* you can add your own scripts into a new bin, and then add this bin's directory to the search path such as:
**$ cd ; mkdir bin ; mv nusers bin; $ cd ; mv nusers bin ; PATH=$PATH:$HOME/bin ; nusers**

### 2.6 Accessing Shell Script Arguments
**Positional Parameters** represet command-line arguments. They also represent a function's arguments within shell functions.
They ese numbers to represent the index of argument: ```$1 $2 ${10}```. For historical reason, you have to enclose the number in braces if it's greater then 9.

For example, if we want to create a shell script help us to find a user who's logged in the system, we can do something like:

```
$ cat > finduser
#! /bin/sh

who | grep $1
^D

$ chmod +x finduser
$ ./finduser ruthnot
$ ./finduser bethy
``` 
* We use **$1** to represent the first argument we typed in the command line
* Anytime you want to do searching, that's a job for the **grep** command, which stands for "global regular expression print", to print all lines matching
a certain pattern.

### 2.7 Simple Execution Tracing

Execution tracing is a option that if you turn on, the output of the shell script will include each step of the actual execution, so that you can see what the 
script is actually doing without opening the script.

* Use "set -x [filename]" to turn on the execution tracing
* Within the script, use "set -x" to turn on, and "set +x" to turn off the execution tracing

Example:
```
$ cat > trace1.sh
#! /bin/sh

set -x
echo 1st echo

set +x 
echo 2nd echo
^D

$ chmod +x trace1.sh
$ ./trace1.sh
```  
And the result will look like:

```
+ echo 1st echo
1st echo
+ set +x
2nd echo
```

After the "+" plus symbole is what the script is executing.

