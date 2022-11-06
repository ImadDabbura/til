Tuples are much faster to create because Python cache them at runtime and doesn't communicate with the OS to allocate memory as it does for the lists.
- Tuples can be constant folded:
```python
dis.dis("(1, 2)")
  1           0 LOAD_CONST               0 ((1, 2))
              2 RETURN_VALUE

dis.dis("[1, 2]")
  1           0 LOAD_CONST               0 (1)
              2 LOAD_CONST               1 (2)
              4 BUILD_LIST               2
              6 RETURN_VALUE
```
- Tuples can be reused instead of copied:
```python
t = (1, 2)
tuple(t) is t =>  True

l = (1, 2)
list(l) is l =>  False
```
- Tuples are compact and don't over-allocate:
```python
sys.getsizeof(tuple(iter(range(10)))) => 120
sys.getsizeof(list(iter(range(10)))) => 136
```
- Tuples directly reference their elements::
    - Tuples refer directly to their elements; references to objects are incorporated directly in a tuple object. In contrast, lists have an extra layer of indirection to an external array of pointers. This gives tuples a small speed advantage for indexed lookups and unpacking:
Here is how the tuple (10, 20) is stored:
```C
    typedef struct {
        Py_ssize_t ob_refcnt;
        struct _typeobject *ob_type;
        Py_ssize_t ob_size;
        PyObject *ob_item[2];     /* store a pointer to 10 and a pointer to 20 */
    } PyTupleObject;
```
Here is how the list [10, 20] is stored:
```C
    PyObject arr[2];              /* store a pointer to 10 and a pointer to 20 */

    typedef struct {
        Py_ssize_t ob_refcnt;
        struct _typeobject *ob_type;
        Py_ssize_t ob_size;
        PyObject **ob_item = arr; /* store a pointer to the two-pointer array */
        Py_ssize_t allocated;
    } PyListObject;
```
