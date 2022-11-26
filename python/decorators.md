Decorator changes the behavior of a function by doing something before calling the function and/or doing/or another thing after calling it. However, **it does not affect the body of the main function that is being decorated.**

```python
@decorator
def func():
    pass
```
is the same as
```python
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

We can also have decorators that take optional arguments:
```python
# Here _func is positional-only argument and num_times is keyword-only argument
def repeat(_func=None, *, num_times=1):
    def decorator_repeat(func):
        @functools.wraps(func)
        def wrapper_repeat(*args, **kwargs):
            res = 0
            for _ in range(num_times):
                res += func(*args, **kwargs)
            return res
        return wrapper_repeat
    
    # If the decorator is called with arguments
    if _func is None:
        return decorator_repeat
    else:
        return decorator_repeat(_func)

@repeat
def add(x, y):
    return x + y
add(10, 10)         #=> 20

@repeat(num_times=3)
def add(x, y):
    return x + y
add(10, 10)         #=> 60
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
