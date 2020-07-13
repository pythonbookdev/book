# Production Ready Python

Welcome to Production Ready Python. This book's focus is on the structure of large Python programs, commonly used language features and data structure libraries, and helping you write maintainable, testable and production ready code.

### Intended Audience

The desired outcome is to make you comfortable with backend Python code for your day job in the least amount of time. You should be able to read and grok a large codebase, contribute a clean, well tested, debuggable, maintainable, and Pythonic feature to it, and effectively debug issues in it after launch.

Additionally, after this book, you should feel comfortable using Python in technical interviews.

The book is targeted towards learners who know basic Python - those who can already manipulate simple data structures like lists, and can write simple programs.

### Material

* We target Python 3, since Python 2 has reached its end of life
* We try to stick to standard library modules as much as possible, with a few exceptions like `requests` due to their ubiquity

**Concepts covered:**

* Python code formatting and style guides
* Quick recap on data structures like `list`, `dict`, and `set` 
* The `collections` module and some commonly used data structures like `defaultdict`, `namedtuple` 
* Context managers - the `with` statement
* File I/O. Reading and writing a common format like `JSON` 
* Exceptions. Best practices for handling exceptions in production code
* Testing via `pytest` . Best practices for writing tests, and appropriate use of `mock` and `mock.patch` 
* Writing effective scripts -- parsing arguments and subprocess calls
* `requests` for HTTP
* `pip` and `virtualenv` for external dependencies
* Code organization, Pythonic code, and conventions -- designing for debuggability
* Effective Logging
* Typing in Python and Mypy

This book is geared towards teaching concepts that we've seen commonly used in large Python codebases. For example, we've rarely seen use of functional operators like `map/reduce/filter`, so those will be omitted here. This will reduce superfluous material you need to learn.

Finally, we will give unique insights into our experience of managing large scale Python backend applications when relevant.

### Open Source

This book is [open source](https://github.com/pythonbookdev/book) and welcomes contributions. For larger changes, like adding a new section, make a Github Issue for discussion, and directly send a pull request for small changes.

### Feedback

Please use Github Issues for general feedback, or send a message on [Twitter](https://twitter.com/ukshah2).

