I/O redirection is very useful especially when we want to disgard errors our redirect output of a some shell command/program to a file. There are three kinds of redirections:

- Redirect stdin fd to a file such as `cat < file`
    - The file descriptor that we want to redirect has to be infront of `<`. In the case of redirecting stdin, `0<` is the same as `<`.
- Redirect stdout/stderr to a file such as `ls dir > tmp` or `ls dir 2>error`
    - The file descriptor that we want to redirect has also to be in the front of `>`. In the case of redirecting stdout, `2>` is the same as `>`.
    - If we want to redirect some file descriptor fd0 to another file descriptor fd1, we can do `fd0>fd1>`.
    - `>` truncates the file we're redirecting the output to and writes the new output
    - `>>` appends to  the file we're redirecting the output to, and doesn't overwrite the old context. Example: `cat /etc/passwd >> tmp`.
