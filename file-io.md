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



