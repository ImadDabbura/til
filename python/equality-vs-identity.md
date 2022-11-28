Every thing in Python is an object. Variables are nothing but pointers to those
objects. Therefore, multiple variables can point to the same object. Therefore:

- To test whether two variables point to the same object, we use `is` operator.
  If the return value is `True` -> both variables point to the same object.
  This can also be tested in CPython using `id()`.
- To test if both variables (object they point to) have the same content, we
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
