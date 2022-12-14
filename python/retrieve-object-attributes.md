When we try to get any object's attributes such as `obj.x`, the interpreter
follow more or less the following steps:

- It invokes `__getattribute__` special method on the instance. If it fails,
- It invokes `__getattr__` special method. It it fails,
- It returns `AttributeError`

```python
class C:
    def __init__(self, x):
        self.x = 10
    
    def __getattribute__(self, k):
        print("getattribute")
        return super().__getattribute__(k)
    
    def __getattr__(self, k):
        print("getattr")
        return super().__getattr__(k)
```

When we want to check if an object has a specific attribute, we can use
`hasattr(obj, "attribute")`, which follows the same logic as above to test if
the object has the given attribute.
