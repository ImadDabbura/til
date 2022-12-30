Instead of creating a class to implement the context manager protocol
(`__enter__` & `__exit__`), we can use `@contextmanager` from `contextlib`
library to decorate any generator function with a single `yield` statement.
This done by wrapping the function in a class that implements the `__enter__`
and `__exit__` methods.

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
    - Invoke the generator function and store the generator object, for example
      `gen`
    - Calls `next(gen)` so the body of generator gets executed until `yield`
      statement
    - Returns the value returned by `yield` so it can used to bound it to the
      target variable of `with`. Therefore, `yield` produces values we want `__enter__` to return and evaluation stops
- Continue evaluating the body of the `with` block
- Once we are done from `with` block (exit `with` block), execution continue
  after the `yield` statement
    -  Checks if there is exception raised in `exc_type` inside `with` block. If
       there is exception, then invoke `gen.throw(exception)` in the `yield`
       line inside the generator function
    - Else, it would invoke `next(gen)`, which makes the generator to continue
      execution after the `yield` line
