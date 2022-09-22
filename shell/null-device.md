`/dev/null` is the null device. It is very useful when we want to discard output of any operation or we want truncate a file. This is due to the fact reading/writing to `/dev/null` has no effect. In the case of reading, it generates end of file right away.

To discard stderr, which has file descriptor 2, we can use the following redirection:
```bash
ls -l dir 2>/dev/null
```

To truncate a file, instead of `rm` and then `touch`, we can use:
```bash
cat /dev/null > file-to-truncate
```
