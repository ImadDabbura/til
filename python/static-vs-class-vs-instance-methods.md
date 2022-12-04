A Python class can have three kinds of methods:

```python
class C:
    
    def instance_method(self):
        pass
    
    @classmethod
    def class_method(cls):
        pass
    
    @staticmethod
    def static_method():
        pass
```
- **Instance method** is a function that is bound to the instance itself and
  the first argument will always be the instance object `self`. It has access
  to both instance and class variables. Most methods inside the class are
  typically instance methods.
- **Class method** is a function that is bound to the class ONLY and the first
  argument will always be the class object itself `cls`. It has access ONLY to
  the class variables. It is typically used as a factory method.
- **Static method** is like a plain function that is not bound to neither
  classs nor instance and doesn't depend on the state of the object. Therefore,
  it doesn't have access to any class or instance variables. It is typically 
  used if it is very close to the class but not exactly belongs to it and is 
  not used from outside the class.
