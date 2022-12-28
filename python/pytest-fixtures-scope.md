Fixtures are functions decorated by `pytest.fixture()` that run before/after test functions by `pytest` to do
the setup/teardown. Test functions as well as other fixtures can depend on
fixtures through their parameter list that would have the same name(s) of the
fixture(s). 

Scopes of fixtures:

- **Function** (default): The setup/teardown runs before/after every run of the
  test function or fixture that depends on it
- **Class**: The setup/teardown runs before/after once for all the test methods
  inside a class
- **Module**: The setup/teardown runs before/after once for all the test functions/methods
  inside a module
- **Package**: The setup/teardown runs before/after once for all the test
  functions/methods inside a package or test directory
- **Session**: The setup/teardown runs before/after once for all the test
  functions/methods inside per session

A fixture can only depend on another fixture that is at the same
scope level of wider. Also, for *package/session* scopes, the fixtures have to
be defined inside `conftest.py` that will be read by `pytest` before running
tests inorder to be actually at the *package/session* level; otherwise, they
will default to the module.
