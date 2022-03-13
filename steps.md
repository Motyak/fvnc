# 1) Init a folder as a fvnc project (inside it)
```console
user@host:~/project$ fvnc init
Select a programming language (c/cpp/js/pl/py/sh) : 
> cpp
Select a C++ compiler (g++/clang) : 
> g++
This folder is now a C++ fvnc project!
user@host:~/project$ ls -AR
.:
c.cpp  .conf  docs  tests  .tools

./docs:

./tests:

./.tools:
activate.sh  soukets  test.pl
```

## Project structure
- c.cpp: the code that will contain the program to run, default is an auto-generated echo program.

- .conf: project configuration file that contains the code to compile/run, the compiler/interpreter to use, ...

- docs/: folder that will contain the html documentation for the program

- tests/: folder that will contain all the tests written by the user in the format 'testname.txt' for the input and 'testname_out.txt' for the expected output.

- .tools/: folder that contains all the framework tools to help with the development.

- .tools/activate.sh: activate the virtual environment to call the commands 'run', 'runtests', 'runasservice', 'viewdoc' and 'deactivate'

- .tools/soukets: program used to expose a program as a service over a TCP socket.

- .tools/test.pl: script that will test the function called in the c.cpp main, based on the files inside the 'tests' folder.

# 2) Enter the project virtual environment
```console
user@host:~/project$ source .tools/activate.sh
(project) user@host:~/project$
```

# 3) Run the default 'echo' program as demo
```console
(project) user@host:~/project$ run
> hello world
hello world
(project) user@host:~/project$
```

# 4) Run the tests as demo
```console
(project) user@host:~/project$ runtests
Nothing to test. (The 'tests' folder is empty)
(project) user@host:~/project$
```

# 5) Write a first test as demo
```console
(project) user@host:~/project$ nano tests/simpleadd.txt
>>> 5 3
(project) user@host:~/project$ nano tests/simpleadd_out.txt
>>> 8
(project) user@host:~/project$
```

# 6) Rerun the tests as demo
```console
(project) user@host:~/project$ runtests
Test 'simpleadd' is failing:
-Expected:
'''
8

'''
-Had:
'''
5 3

'''
(project) user@host:~/project$
```

# 7) Fix the code to make the test pass
Here we will just create an 'add' function and call it in the main.

# 8) Rerun the tests as demo
```console
(project) user@host:~/project$ runtests
1/1 test(s) has passed
(project) user@host:~/project$
```

# 9) Run the updated program and give it a try
```console
(project) user@host:~/project$ run
> 10 89
99
(project) user@host:~/project$
```

# 10) Expose the program as a service and give it a try
```console
(project) user@host:~/project$ runasservice -p9191
(project) user@host:~/project$ echo "10 89" | curl -s 127.0.0.1:9191
99
(project) user@host:~/project$
```

# 11) Show the auto-generated doc
```console
(project) user@host:~/project$ viewdoc
Opening the documentation in your default web browser...
(project) user@host:~/project$
```

# 12) Leave the project virtual environment
```console
(project) user@host:~/project$ deactivate
user@host:~/project$
```
