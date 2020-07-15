# Lambdas and Callables

### Callables

A callable is anything that can be called. Let's see an example:

```python
def greet():
    print("Hello")

# g is callable
assert callable(greet)

# g is just another object
assert isinstance(greet, object)

greet()
```

It's also possible to make regular [objects](https://stackoverflow.com/questions/111234/what-is-a-callable) \(instances of a `class` \) callable, but we rarely need to do that, so we're omitting that here. On the other hand, it's often useful to create a function on the fly. 

The builtin types are callables too. Calling them returns the default value of their type.

```text
>>> assert callable(str)
>>> assert str() == ''
>>> assert int() == 0
```

### Lambdas

Let's say we want to make a simple calculator: 

```python
def calculate(operation: str, a: int, b: int):
    if operation == '+':
        return a + b
    elif operation == '-':
        return a - b
    elif operation == '*':
        return a * b
    elif operation == '/':
        return a / b
    else:
        raise ValueError('Invalid operation provided', operation)
```

This example is simple, but you could imagine that for a more complex calculator, we'd want to separate the actual operation implementation into separate methods.

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b
    
def divide(a, b):
    return a / b


def calculate(operation: str, a: int, b: int):
    if operation == '+':
        return add(a, b)
    elif operation == '-':
        return subtract(a, b)
    elif operation == '*':
        return multiply(a, b)
    elif operation == '/':
        return divide(a, b)
    else:
        raise ValueError('Invalid operation provided', operation)
```

The other benefit of separating out each method is that we can get rid of the if/else and replace it with a dictionary lookup:

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b
    
def divide(a, b):
    return a / b


def calculate(operation: str, a: int, b: int):
    operations = {
        '+': add,
        '-': subtract,
        '*': multiply,
        '/': divide
    }
    
    if operation in operations:
        function = operations[operation]
        return function(a, b)
    else:
        raise ValueError('Invalid operation provided', operation)
```

It might seem weird to put a method as a dictionary value, but it's an illustration of the extremely dynamic nature of the language. **A method is just another object that is callable.** 

This definitely seems cleaner, but it seems overkill to move these really simple methods to their own method definition. That's where `lambda` comes in. `lambda` lets you define a quick, anonymous function that does one statement worth of work. Which is exactly what we need here.

```python
def calculate(operation: str, a: int, b: int):
    operations = {
        '+': lambda a, b: a + b, # take two arguments, a and b. Return a + b
        '-': lambda a, b: a - b,
        '*': lambda a, b: a * b,
        '/': lambda a, b: a / b
    }
    
    if operation in operations:
        function = operations[operation]
        return function(a, b)
    else:
        raise ValueError('Invalid operation provided', operation)
```

A lambda always returns whatever it computes. More examples:

```python
lambda: None # no-op lambda
lambda: greet() # calls the greet function
```

Lambas are useful in places that you need to pass in a  `Callable` for any reason. You will see more examples of these in the rest of the course.

