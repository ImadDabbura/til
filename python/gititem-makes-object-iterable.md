Any object that implement `__getitem__` special method is iterable and you can use `in` operater to check if an item is in the object even if the object doesn't impelement `__contain__` special method.
- Python generate indexes starts from zero and iterate over all items until the object returns Error -> Stop Iteration
    - The main assumption is that the object takes integers as indices
- To check if an item is in the object, Python iterates over all items (using the above method)
