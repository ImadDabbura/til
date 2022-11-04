Whenever a variable, function, or module is invoked in Python, there is a hierarchy that determines where it looks for these objects. 

- First, Python looks inside the `locals()` array, which has entries for all local variables. Python works hard to make local variable lookups fast, and this is the only part of the chain that doesn’t require a dictionary lookup. 
    - `__local variables__` do not need a dictionary lookup to be found; they are stored in a very slim array that has very fast lookup times. Because of this, finding the function is quite fast!
- If it doesn’t exist there, the `globals()` dictionary is searched. 
- Finally, if the object isn’t found there, the `__builtin__` object is searched. 

It is important to note that while `locals()` and `globals()` are explicitly dictionaries and `__builtin__` is technically a module object, when searching `__builtin__` for a given property, we are just doing a dictionary lookup inside its `locals()` map (this is the case for all module objects and class objects!).

As a result of the above:

- It is recommended to import specific objects (variables/functions/classess...) from a `module` instead of just importing the `module` and use the `module` name to refer to the objects it contains because this will slow down the run-time.
- The performance of the dictionary lookup is largely dependent of the `hash` function. Therefore, the slower the hash function, the slower the lookup and may not have __O(1)__ lookup anymore.

