---
 	layout: post
 	title: styleguide-Style-guides-for-Google-originated-open
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# styleguide-Style-guides-for-Google-originated-openAll new code should contain the following and existing code should be updated to be compatible when possible:
```
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function
```
If you are not already familiar with those, read up on each here: [absolute imports](https://www.python.org/dev/peps/pep-0328/), [new `/` division behavior](https://www.python.org/dev/peps/pep-0238/), and [the print function](https://www.python.org/dev/peps/pep-3105/).
### 2.21.1 Definition
Type annotations (or “type hints”) are for function or method arguments and return values:
```
def func(a: int) -> List[int]:
```
You can also declare the type of a variable using a special comment:
```
a = SomeFunc() # type: SomeType
```
### 2.21.2 Pros
Type annotations improve the readability and maintainability of your code.
```
import collections
import queue
import sys
from absl import app
from absl import flags
import bs4
import cryptography
import tensorflow as tf
from book.genres import scifi
from myproject.backend.hgwells import time_machine
from myproject.backend.state_machine import main_loop
from otherproject.ai import body
from otherproject.ai import mind
from otherproject.ai import soul
# Older style code may have these imports down here instead:
#from myproject.backend.hgwells import time_machine
#from myproject.backend.state_machine import main_loop
```
### 3.14 Statements
Generally only one statement per line.
```
Yes:
if foo: bar(foo)
```
```
No:
if foo: bar(foo)
else: baz(foo)
try: bar(foo)
except ValueError: baz(foo)
try:
bar(foo)
except ValueError: baz(foo)
```
### 3.15 Accessors
If an accessor function would be trivial, you should use public variables instead of accessor functions to avoid the extra cost of function calls in Python.
Example:
```
from typing import List, TypeVar
T = TypeVar("T")
...
def next(l: List[T]) -> T:
return l.pop()
```
A TypeVar can be constrained:
```
AddableType = TypeVar("AddableType", int, float, Text)
def add(a: AddableType, b: AddableType) -> AddableType:
return a + b
```
A common predefined type variable in the `typing` module is `AnyStr`.
```
from typing import Text, Union
...
def py2_compatible(x: Union[bytes, Text]) -> Union[bytes, Text]:
...
def py3_only(x: Union[bytes, str]) -> Union[bytes, str]:
...
```
If all the string types of a function are always the same, for example if the return type is the same as the argument type in the code above, use [AnyStr](http://google.github.io/styleguide/pyguide.html).
Ex:
```
from typing import Any, Dict, Optional
```
Given that this way of importing from `typing` adds items to the local namespace, any names in `typing` should be treated similarly to keywords, and not be defined in your Python code, typed or not.
