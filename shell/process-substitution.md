`<(CMD)` is called **process substitution**,  which will execute `CMD` and
place the output in a temporary file and substitute the `<()` with that file’s
name. This comes in handy because some commands such as `diff` expect values
to be passed as files instead of standard input. For example, `diff <(ls dir1)`
<(ls dir2) will show differences between files in `a` & `b` directories.
