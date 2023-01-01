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
