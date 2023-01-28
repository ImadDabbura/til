Python follows more or less the following steps when looking up an attribute inside of an object:

- First looks at `obj.__dict__[attribute]`. If it is not found, 
- Then looks at `type(obj).__dict__[attribute]`. If it is not found, 
- Check `__dict__` of all the superclasses. 

However, if Pythons see that the attribute is implemented using a descriptor, it uses the descriptor methods (`__get__`).
