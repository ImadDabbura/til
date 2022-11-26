A **closure** is a function that retains the bindings of the free variables
that exist when the function is defined, i.e. it would maintain a refernce to
the free variables that can be used when the function is invoked later.

```python
def func(x):
    y = 100
    def nested_func(z):
        return x + y + z
    return nested_func

f = func(10)
print(f.__closure__)            #=> (<cell at 0x7fd10dc26830: int object at 0x7fd108a00210>, 
                                #=>  <cell at 0x7fd10d7abe50: int object at 0x7fd108a00d50>)
print(f.__code__.co_freevars)   #=> ('x', 'y')
f(10)                           #=> 120
```

`x` and `y` are free variables here. Each object `f.__closure__` corresponds to a name in the
`f.__code__.co_freevars`.

This is in some way similar to decorators where the decorated function is
nothing but the nested function, which can be written in the following form:

```python
def func(x):
    def decorator_func(func):
        y = 100
        def wrapper_func(z):
            return func(z) + x + y
        return wrapper_func
    return decorator_func

@func(10)
def nested_func(z):
    return z

nested_func(10)     #=> 120
```
