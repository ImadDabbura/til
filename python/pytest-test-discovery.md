Test discovery process in `pytest` goes as follows:

- It recursively looks for files in the given directories (use current working
  directory if no directory/file is given) and all their subdirectories that
  named with `test_*.py` or `*_test.py`.
- In each of the test files identified, it looks for functions/methods that
  start with `test_` and classes that start with `Test`

We can always run tests in specific file by running `pytest file` or specific
test in a test file `pytest path/to/file::test_name`
