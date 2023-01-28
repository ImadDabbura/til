`@property` implements full descriptor protocol (class that implements a dynamic protocol consisting of `__set__`, `__get__`, and `__delete__`) that shadows instance attributes of the same name
when we try to access/set/delete instance attributes.

The signature of `property` constructor is `property(fget=None, fset=None,
fdel=None, doc=None)`. Few important things about instance attributes decorated
by `@property`:

- If the attribute doesn't have setter -> read-only attribute
- If the attribute doesn't have deleter -> we can't delete the attribute

 ```python
class C:
    def __init__(self):
        self._x = 10

    @property
    def x(self):
        # called when we use obj.x
        return self._x

    @x.setter
    def x(self, v):
        # called when we use obj.x = v
        self._x = v

    @x.deleter
    def x(self, v):
        # called when we use obj.x = v
        self._x = v
 ```

