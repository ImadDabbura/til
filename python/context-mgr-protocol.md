`with` statement is designed to work with context manager objects to simplify
the `try/finally` pattern, which guarantees that some code is executed (clean
up code) after the `with` block code is aborted because of an exception, a
`return` or `sys.exit()` call. In a sense, the clean-up that would typically be
in the `finally` clause such as releasing some resources or restoring the
temporarily changed state.

Context manager protocol implements `__enter__` & `__exit__`:

- `__enter__` will be invoked on the object after `with` keyword, which is
  called the context manager object. It takes no arguments.
- The value `__enter__` returns, which could be `None`, `self`, or any other
  value would be assigned to the target variable that comes after `as`
  keyword.
- Once the `with` code block is terminated for any reason, `__exit__` is
  invoked on the context manager object, which takes 3 arguments (all default
  to `None`):
    - `exc_type`: Exception type such as `ValueError`
    - `exc_val`: Exception object`
    - `traceback`: Traceback object

```python
class ContextProtocal:
    def __enter__(self):
        # Setup
        # return nothing, i.e. None
        # Or return self
        return self

    def __exit__(self, exc_type, exc_val, traceback):
        # Teardown which should typically handle exceptions
        # to make sure the  Teardown is taken care of even
        # in the case of exceptions
        pass
```
