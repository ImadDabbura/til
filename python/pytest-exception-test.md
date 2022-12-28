Tests generally fails for 3 reasons:

- The assetion test fails
- `pytest.fail()` is called with the test
- An exception is raised in the code that is being tested and not handled

We can use `pytest.fail()` to test for exceptions that our code is expected to
raise in certain cases.

We can test if the code raises expected exception (here `ValueError`):

```python
def test_raises_exc():
    with pytest.fail(ValueError):
        fn()
```

We can test if the code raises expected exception and exception message matches
correct message:

```python
# One way
def test_raises_exc():
    msg_regex = "something .* final"
    with pytest.fail(ValueError, match=msg_regex):
        fn()

# Another way
def test_raises_exc():
    with pytest.fail(ValueError) as exc:
        fn()
    expected = "Some exception message"
    assert expected in str(exc.value)
```
