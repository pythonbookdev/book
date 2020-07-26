# File IO

> Prerequisites - Knowing general FileIO concepts like opening and closing as well as read and write modes.

## open

The idiomatic way to open files in python is through the `with` clause.

```python
with open('testfile.txt', 'r') as file:
    print(file.read())
```

Opening the file this way ensures that the file will be closed at the end of the with block. This idiom helps avoid the more painful and verbose `try-finally` construct; which would instead look like this:

```python
file = open('testfile.txt', 'r')
try:
    print(file.read())
finally:
    file.close()
```

On top of being concise, the idiom has the advantage of being intuitive and also helping developers not forget to close the files they open.
The idiom is also flexible enough to be used with two files as the same time:

```python
# A piece of code that reads a file and inverts the order of the lines in it.
with open('input.txt', 'r') as infile, open('output.txt', 'w') as outfile:
    lines = infile.readlines() # readlines returns a List with each element in the list being a line of the file (the element will include the "\n" at the end)
    reversedlines = reversed(lines)
    outfile.writelines(reversedlines)
```

## os module

For other File IO operations like listing directories, copying files, or renaming files the `os` module is the tradional method.

```python
import os

os.rename("oldname", "newname") # Changes the name of a file called "oldname" to "newname"
```

Let us demonstrate some of the methods in the module with an example.
A quick sample code that searches a directory full of text files for a search term and writes out matching lines to an output file.

```python
import os
import os.path

searchterm = "imagineThisIsUserInput"
searchdir = "imagineThisIsUserInputToo"

matchedLines = []

for directoryEntry in os.listdir(searchdir):
    relativePathToEntry = os.path.join(searchdir, directoryEntry)
    if os.path.isfile(relativePathToEntry):
        with open(relativePathToEntry, "r") as infile:
            for line in infile.readlines():
                if searchterm in line:
                    matchedLines.append(line)

with open("output.txt", "w") as outfile:
    outfile.writelines(matchedLines)
```

In this example we explored methods like: `os.listdir`, `os.path.join`, `os.path.isfile` and how to put it all together.
The advantages of using the `os.path` module here include not having to reinvent the wheel when it comes to manipulating paths and making the code more platform independant.

There are several more methods in the modules `os` and `os.path` and the reader is adviced to peruse their official documantation for more examples and tips.