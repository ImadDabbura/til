Decorator changes the behavior of a function by doing something before calling the function and/or doing/or another thing after calling it. However, **it does not affect the body of the main function that is being decorated.**

```python
@decorator
def func():
    pass
```
is the same as
```pythob
func = decorator(func)
```

Boilerplate template for any decorator:
```python
import functools
def decorator(func):
    @functools.wraps(func)
    def wrapper_decorator(*args, **kwargs):
        # Do something
        value = func(*args, **kwargs)
        # Do something
        return value
    return wrapper_decorator
```

If we want the decorator to be stateful, we can use classes as decorators:
```python
class Decorator:
    def __init__(self, func):
        # We can't use @functools.wrap(func)
        functools.update_wrapper(self, func)
        self.func = func
        # keep state here

    def __call__(self, *args, **kwargs):
        # Do something, probably update state
        value = self.func(*args, **kwargs)
        # Do something, probably update state
        return value
```
Don't forget to return the value of decorated function 😀
