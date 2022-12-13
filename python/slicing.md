When we provide a **slice** to any sequence object (object that implements
`__getitem__` and `__len__`), we get back an instance of the same type with the
elements in the slice. Here is how slicing works:

- When we have commas inside `[]`, `__getitem__` gets tuple of `slice`
  object.
- When we have `:` inside `[]`, `__getitem__` gets a `slice` object.

`slice` object has 4 important attributes:

- start
- step
- stop
- indices
