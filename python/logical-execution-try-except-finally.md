The logical execution of try/except/finally/else goes as follows:

```python
try:
    ...
except:
    ...
else:
    ...
finally:
    ...
```
- `try` block gets executed
- If `try` block executes successfully, `else` block starts execution.
- If `try` block raises an `exception`:
    - Exception gets saved and `finally` block gets executed.
        - `exception` gets raised if it wasn't handled
        - If `finally` block returns -> `exception` gets suspended
        - If `finally` raises an exception, the saved exception will be raised
          in the context of the new exception
