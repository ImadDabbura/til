**Command substitution** is very useful when we want to execute a command and
assign its output to a variable. This can be done like this: `$(CMD)`. This 
will execute `CMD`, get the output of the command and substitute it in place.

The following will execute `ls` and assigns the output to the variable `FILES`.

```bash
mkdir test
touch test/{a..c}
FILES=$(ls)
echo FILES
# will print
a
b
c
```
