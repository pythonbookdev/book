# Idiomatic Collections

> Prerequisites - Knowing how basic data structures like `list`, `dict`, `tuple`and `set` work. `args` [and](https://realpython.com/python-kwargs-and-args/) `kwargs`

Most backend tasks can be done with one of the built-in data structures. But sometimes, it's more idiomatic to use a specialized data structure, or there's a need for a special feature, like a dictionary that keeps track of insertion order. We'll be covering some useful modules that fit that bill.

### collections.defaultdict

The `defaultdict` is used in cases where it's preferable to have a default value for dictionary keys rather than dealing with keys with no values. 

Its first argument is a `Callable` that is instantiated and set as the key's value if someone tries to retrieve the key.

```python
>>> from collections import defaultdict
>>> 
>>> # quick refresher: types are also callables
>>> assert 5 == int(5)
>>> assert '' == str()
>>> 
>>> # defaultdict takes a callable
>>> dictionary = defaultdict(str) 
>>> dictionary
defaultdict(<class 'str'>, {})
>>> len(dictionary)
0

>>> # if the key doesn't exist but is accessed, the callable
>>> # is called, and the value is stored for that key
>>> dictionary['hello']
''
>>> dictionary
defaultdict(<class 'str'>, {'hello': ''})
>>>
>>> # setting a value remains the same
>>> dictionary['byebye'] = 'farewell'
>>> dictionary
defaultdict(<class 'str'>, {'hello': '', 'byebye': 'farewell'})

>>> # defaultdict can take a lambda with no args as a default value, 
>>> # since a its just another callable
>>> another_dictionary = defaultdict(lambda: 'default string')
>>> another_dictionary['hello'] += ' another string'
>>> another_dictionary
defaultdict(<function <lambda> at 0x7f1b6a75c670>, {'hello': 'default string another string'})

# since a += involves getting the value, and then setting it,
# this is what's happening:
# another_dictionary['hello'] = another_dictionary['hello'] + ' another string'

# the first another_dictionary['hello'] calls the lambda we passed,
# which returns 'default string'. Then, we finally add it to 
# ' another string' which gives us the final value of both the strings
# together
```

This is useful in cases like performing arithmetic with default values. For example:

```python
from collections import defaultdict

pageviews_raw = [
    ('/', 10),
    ('/home', 5),
    ('/get', 10),
    ('/home', 10),
]

# the non default dictionary way
total_per_page_dict = {}

for item in pageviews_raw:
    url, count = item
    if url not in total_per_page_dict:
        total_per_page_dict[url] = 0
    total_per_page_dict[url] += count

print(total_per_page_dict)

# the default dictionary way
total_per_page_defaultdict = defaultdict(int)

# this loop no longer needs to special case the base case
for item in pageviews_raw:
    url, count = item
    total_per_page_defaultdict[url] += count

assert total_per_page_dict == total_per_page_defaultdict

# outputs: {'/': 10, '/home': 15, '/get': 10}
```

`defaultdict` is also useful to build nested data structures. It lets you skip initializing a nested data structure. For example:

```python
from collections import defaultdict

pageviews_raw = [
    ('/', 10),
    ('/home', 5),
    ('/get', 10),
    ('/home', 10),
]

pageviews_grouped_by_route = defaultdict(list)

for item in pageview_logs:
    url, count = item
    
    # accessing pageviews_grouped_by_route[url]
    # causes either a new list to be created, or
    # to retrieve the list that already exists 
    # for this key
    pageviews_grouped_by_route[url].append(count)

print(pageviews_grouped_by_route)

# defaultdict(<class 'list'>, {'/': [10], '/home': [5, 10], '/get': [10]})
```

### collections.namedtuple

`namedtuple` is a tuple which allows idiomatic creation and use of a tuple. It's used when someone wants to pass around an immutable collection of data. Let's see an example:

```python
>>> from collections import namedtuple
>>>
>>> # define a new namedtuple called 'PageViews'
>>> PageViews = namedtuple('PageViews', ['page', 'view_count'])
>>>
>>> # all values are required by default
>>> PageViews()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __new__() missing 2 required positional arguments: 'page' and 'view_count'
>>> 
>>> # args will be parsed in order
>>> PageViews('/', 2)
PageViews(page='/', view_count=2)
>>>
>>> # kwargs also work, and just like for any kwargs, they can be passed
>>> # in any order
>>> PageViews(view_count=2, page='/')
PageViews(page='/', view_count=2)
>>>
```

{% hint style="warning" %}
It's not recommended to use namedtuple unless you need compatibility with existing tuples.
{% endhint %}

`namedtuple` is often inflexible and can cause more pain than actually add value.

`namedtuple` requires every member to be explicitly initialized, so adding a new value to an existing named tuple requires significant refactoring. For example, let's say that a `namedtuple` happens to be an argument to a commonly used function, where callers initialized the tuple on the fly. If we wanted to add a new, optional parameter to the namedtuple, we would have to refactor every caller to include a value for this parameter \(and we wouldn't be able to set a default\). This is extremely similar to adding a new argument to a method \(instead of a keyword argument\).





