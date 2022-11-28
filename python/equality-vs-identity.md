Every thing in Python is an object. Variables are nothing but pointers to those
objects. Therefore, multiple variables can point to the same object. Therefore:

- To test whether two variables point to the same object, we use `is` operator
  which compares the identity of both variables. If the return value is `True` -> both variables point to the same object.
  This can also be tested in CPython using `id()`.
- To test if both variables (objects they point to) have the same content, we
  use `==` operator.

```python
a = [2]
b = a
a is b          #=> True
id(a) == id(b)  #=> True


a = [2]
b = [2]
a is b          #=> False
id(a) == id(b)  #=> True
```

Note: It is recommended to use `is` operator when checking if a variable is: `True`, `False`, or `None`. If we use `==`, it will invoke `__eq__` method, which if not implemented, compare the ids of both variables and is slower than `is` operator because it first has to look up `__eq__` method and then invoke `id()` on both variables.
