Typically all attributes are stored in the instance's dictionary `__dict__`.
This will add space overhead due to the hash table being sparse. We can save
memory by storing all the attributes in a tuple-like data structure using
`__slots__` at the beginning of the class definition (see below):

```python
import sys


class C:
    def __init__(self, x, y):
        self.x = x
        self.y = y

class C_Slots:
    __slots__ = ("x", "y")

    def __init__(self, x, y):
        self.x = x
        self.y = y

print(sys.getsizeof(C))         #=> 904
print(sys.getsizeof(C_Slots))   #=> 1,072
```

The main problems with `__slots__`:

- Can't dynamically add attributes to the instance. We can work around this
  issue by adding `__dict__` to `__slots__` but this negates the benefits of
  using `__slots__`.
- Doesn't support `__weakref__` by default. We need to add `__weakref__` to
  `__slots__` to be able to use it.
- All sublcasses have to declare `__slots__` because attributes can't be
  inheritted and will be ignored by the interpreter.

In conclusion, use `__slots__` only if it is justified.
