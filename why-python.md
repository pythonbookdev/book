# Why Python?

Why would someone write a production application in Python?

### **Advantages**

**Ease of Use:** Python is an extremely easy language to learn.

**Community:** There's a lot of high quality, supported, and open source libraries for most requirements to run a production application. For example, there's battle tested projects with hundreds of thousands of users for [running](https://www.google.com/search?q=flask+python&oq=flask+&aqs=chrome.1.69i57j0l7.1725j0j7&sourceid=chrome&ie=UTF-8) web [servers](https://www.djangoproject.com/) and interacting with [databases](https://www.sqlalchemy.org/).

![There&apos;s a module for everything. credit: xkcd.com](https://imgs.xkcd.com/comics/python.png)

What this means is it's extremely easy to build early versions of most applications with Python.

### Disadvantages

Conversely, let's explore why someone would _not_ want to write a production application in Python:

**Performance:** Python is a slow language. If you expect to do any serious computation work in your application, Python might not be the right fit.

**Organizational scalability:** Python does not require users to specify types up front - it's a dynamically typed language. Let's explore that difference really quickly: in Java, if you want to specify a list of numbers, you need to specify its type. For example:

Java

```java
List<Integer> numbers = new ArrayList<Integer>(1, 2, 3);

numbers.add("not a number"); 

// this code would not compile, since we're trying to add
// a string to a list of Integers
```

Python

```python
numbers = [1, 2, 3] # no type required
numbers.append("not a number") # Python allows this

for i in numbers:
    print(i + 1)

# when you run this in a terminal, the output would be:

2
3
4
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
TypeError: cannot concatenate 'str' and 'int' objects
```

Since Python doesn't require you to specify types, it's easier to add bugs to code that won't be caught by the compiler, and will only show up when you run code. With more and more engineers contributing to the same codebase, each individual engineer has less knowledge of existing code. So they might try to add a string to a list of numbers. And if there's no tests added to this code, this will become a user facing bug, which creates a worse user experience, and is harder to track down. So compiled languages generally let many engineers contribute to the same codebase while providing a larger sense of safety, since the compiler will catch many basic errors.

### What this means in practice

Many large applications - like Instagram, YouTube, and Dropbox - start off as one large Python web application \(a monolith\). With good practices around testing and a small team, it's easy to write a production application that's "good enough" for tens of thousands of users. Eventually, components of these websites get separated out into different services, often written in compiled languages for better performance and safety guarantees from the compiler, and better organizational scalability. For example, YouTube talks to its databases via [Vitess](https://vitess.io/), a service written in Go. 

Additionally, with new language features like [type hints](https://docs.python.org/3/library/typing.html), a lot of the benefits of static typing can be applied to Python, so that it can scale to more engineers. Still, some features of Python can easily let users cause large technical debt down the road, like allowing circular imports. We'll discuss this more in detail later.

