# The collections module

> Prerequisites - Knowing how basic data structures like `list`, `dict`, `tuple`and `set` work.

Most standard back-end tasks require one of the inbuilt data structures. But sometimes, it's more idiomatic to use a particular data structure, or there's a requirement for a special property, like a dictionary that keeps track of insertion order. We'll be covering some useful modules from the `collections` module that fit that bill.

### defaultdict

The `defaultdict` is used in cases where it's preferable to have a default value for dictionary keys rather than dealing with keys with no values. 

Its first argument is a `Callable` that is instantiated and set as the key's value if someone tries to retrieve the key.

```python
>>> from collections import defaultdict
>>> dictionary = defaultdict(str) # str is a callable, since you can do str() and get back a string
>>> dictionary
defaultdict(<class 'str'>, {})
>>> len(dictionary)
0

# automatic creation on retrieving a key
>>> dictionary['hello']
''
>>> dictionary
defaultdict(<class 'str'>, {'hello': ''})
>>> len(dictionary)
1
>>> dictionary['byebye'] = 'farewell'
>>> dictionary
defaultdict(<class 'str'>, {'hello': '', 'byebye': 'farewell'})

# Advanced concepts ahead. Read this if you understand lambdas and callables

# defaultdict can take any lambda as a default value, since a lambda is
# just another callable
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

This is useful in cases like performing arithmetic with default values. For example

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
# {'/': 10, '/home': 15, '/get': 10}


#
# ==================================
#


# the default dictionary way
total_per_page_defaultdict = defaultdict(int)

# this loop no longer needs to special case the base case
for item in pageviews_raw:
    url, count = item
    total_per_page_defaultdict[url] += count

assert total_per_page_dict == total_per_page_defaultdict
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





