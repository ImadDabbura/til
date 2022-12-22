Below are different ways of running subsets of test in `pytest`:

- Test method inside TestClass: `pytest
  path/test_module.py::TestClass::test_method`
- All tests in TestClass: `pytest path/test_module.py::TestClass`
- Test function: `pytest path/test_module.py::test_function`
- All tests a file: `pytest path/test_module.py`
- All tests in a directory (and its subdirectories): `pytest path`
- Tests matching a name pattern: `pytest -k pattern`
    - We can use `not`, `and`, `or` inside regex pattern
    - Examples:
        - `pytest -k forward` would run all tests that have *forward* in their
          name.
        - `pytest -k "forward and not forward_backward"` would run all tests that
          have *forward* in their name but not *forward_backward*.
        - `pytest -k "forward or backward and not forward_backward"` would run
          all tests that have *forward* or *backward* in their name but not
          *forward_backward*.
