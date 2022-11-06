**Tuples** and **Lists** are referential data structures (container sequence), which means each element in them is just a pointer to objects but not the objects themselves. This is what allowed them to contain elements of different types. Compare that with **arrays** (**flat sequence**) that hold the actual elements, which requires all elements to be of the same type.

They share some of the same characteristics such as search time which is *O(n)*. However, there are some differences that makes *tuples* in certain circumstances as is seen in the Python interpretter especially when the object's size is not expected to change.

- Lists are **mutable** but tuples are **immutable**. This means that we can't delete or replace elements in tuples or extend/shrink its size.
- Tuples are much faster to create because Python cache them at runtime and doesn't communicate with the OS to allocate memory as it does for the lists.
```python
%timeit l = [0,1,2,3,4,5,6,7,8,9] #=> 60.5 ns ± 0.357 ns per loop (mean ± std. dev. of 7 runs, 10,000,000 loops each)
%timeit t = (0,1,2,3,4,5,6,7,8,9) #=> 11.9 ns ± 0.255 ns per loop (mean ± std. dev. of 7 runs, 100,000,000 loops each)
```
- Tuples can be constant folded: Python interpretter generates bytecode for a tuple in one operation, but generates bytecode for each element is the list as a seperate operation then pushes it to data stack.
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
- Tuples can be reused instead of copied: If a tuple is hashable, `tuple(t)` returns itself because it should stay fixed. On the other side, `list(l)` would return new copy.
```python
t = (1, 2)
tuple(t) is t #=>  True

l = (1, 2)
list(l) is l #=>  False
```
- Tuples are compact and don't over-allocate.
```python
sys.getsizeof(tuple(iter(range(10)))) #=> 120
sys.getsizeof(list(iter(range(10)))) #=> 136
```
- Tuples directly reference their elements: references to objects are incorporated directly in a tuple object. In contrast, lists have an extra layer of indirection to an external array of pointers. This gives tuples a small speed advantage for indexed lookups and unpacking:
    - Here is how the tuple (10, 20) is stored:
    ```C
    typedef struct {
        Py_ssize_t ob_refcnt;
        struct _typeobject *ob_type;
        Py_ssize_t ob_size;
        PyObject *ob_item[2];     /* store a pointer to 10 and a pointer to 20 */
    } PyTupleObject;
    ```
    - Here is how the list [10, 20] is stored:
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
**Conclusion**: Use tuples as immutable lists to 1) clarify that its length won't change and 2) get a little of speed up due to some optimizations the Python interpretter may do as a result of some of the above.
