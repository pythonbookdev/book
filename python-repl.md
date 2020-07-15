# The Python REPL

### What's a REPL?

Python is an interpreted language. Which means Python reads code files line by line and executes it on the fly. For example, let's say you have a source file that looks like this:

```python
# hello_world.py
from time import sleep

print("Hello")

sleep(5) # block for 5 seconds

asdfasdfasdf # NameError: this variable is not defined
```

Python will run the first six lines happily, block for 5 seconds, and only fail when reaching line 8. In another language, like Java, an error like the one on line 8 would fail at the compilation step and would not run at all. 

Given this nature of executing lines of code on the fly, one can imagine writing a program that waits for the user to input a line of code, and once they do so, execute that line, and then wait for the next input. For example:

```text
please enter input > from time import sleep

(importing... done)

please enter input > print("Hello")

Hello

please enter input > exit

Bye
```

This is basically a [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) \(read eval print loop\). It **Reads** code, **Evaluates** it, **Prints** the output, and **Loops.** When you run Python with no arguments, it automatically opens a repl for you. Read [this](https://docs.python.org/3/tutorial/interpreter.html) to learn how to open the Python REPL on your OS.

```python
Python 3.7.4 (default, Sep  7 2019, 18:27:02)
Type "help", "copyright", "credits" or "license" for more information.
>>> print("hello")
hello
>>> 
```

### What's the point?

One of the key advantages of an interpreted language like Python is this repl. You can quickly use it to read documentation and validate your assumptions. For example, if you want to test out the time module, you might do the following:

```python
>>> import time
>>> help(time)

Help on built-in module time:

NAME
    time - This module provides various functions to manipulate time values.

DESCRIPTION
    There are two standard representations of time.  One is the number
    of seconds since the Epoch, in UTC (a.k.a. GMT).  It may be an integer
    or a floating point number (to represent fractions of seconds).
    The Epoch is system-defined; on Unix, it is generally January 1st, 1970.
    The actual value can be retrieved by calling gmtime(0).

<snip>

>>> help(time.sleep)

Help on built-in function sleep in module time:

sleep(...)
    sleep(seconds)

    Delay execution for a given number of seconds.  The argument may be
    a floating point number for subsecond precision.

# verify the syntax
>>> time.sleep(5) 

# just double checking
>>> time.sleep(5, 5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: sleep() takes exactly one argument (2 given)
>>> # okay, now you're ready to use this in your production code
>>> exit()
```

As you can see, this becomes an extremely useful tool to get quick feedback. You can also paste in full functions, classes, or any code you need to manually test quickly.

Every time the REPL is used in the rest of the course, you will see the three `>` signs

```python
>>>
```

