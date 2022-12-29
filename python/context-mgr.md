Instead of creating a class to implement the context manager protocol
(`__enter__` & `__exit__`), we can use `@contextmanager` from `contextlib`
library to decorate any generator function with a single `yield` statement.

```python
def gen():
    # Anything here for the setup
    print("setup")

    # expression after yield will be returned after calling the gen 
    # function in `with` block; otherwise, `None` will be returned
    # equivalent to `__enter__`
    yield

    # Anything here will be part of the teardown when we exit the 
    # `with` block, equivalent to `__exit__`
    print("teardown")

with gen():
    print("inside `with` block")
print("outside `with` block")

# Output
setutp
inside `with` block
teardown
outside `with` block
```

Here is how generator functions decorated with `contextmanager` get evaluated:

- Evaluates the body of the generator function until the `yield` statement
- `yield` produces values we want `__enter__` to return and evaluation stops
- Continue evaluating the body of the `with` block
- Once we are done from `with` block (exit `with` block), execution continue
  after the `yield` statement
