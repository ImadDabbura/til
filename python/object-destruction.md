Every Python object has a `refcount` integer field that counts how many
objects/variables are pointing towards it within the program.

- `refcount` gets incremented when new variable or object points to it
- `refcount` gets decremented when either one the variables/objects that used
  to point to it gets reassigned to point to new object OR we call `del
  obj`

Once the `refcount` reaches zero or the object becomes unreachable (determined
by **mark-sweep** algorithm used by the garbage collector)

- The interpreter will call `__del__` special method for final cleanup before
  destorying the object.
- Its memory will be reclaimed by the interpreter through garbage collector
