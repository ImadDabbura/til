- **Overriding** descriptors are descriptors that implement `__set__`. Therefore, the user can't shadow any attribute that is defined as an overriding descriptor because any assignment at the to the instance's attribute will be forced to go through the `__set__` method. The below class utilizes `@property`, which is an overriding descriptor, to make an attribute as a read-only attribute.

```python
class Test:
    def __init__(self):
        self._x = 1
    
    @propery
    def x(self):
        return self._x

c = Test()
print(c.x)	#=> 1
c.x = 10	#=> AttributeError: can't set attribute 'x'
```
- **Non-overriding** descriptors are descriptors that don't implement `__set__`. This means that the user can shadow the attribute. The common example of a non-overriding descriptor is the instance methods. They are actually implemented using non-overriding descriptor with `__get__` method.

```python
class Test:
    def f(self):
        return 1

c = Test()
type(c.f)	#=> method
print(c.f())	#=> 1

c.f = 0
type(c.f)	#=> int
print(c.f)	#=> 0
```
