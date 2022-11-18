Let's assume that we recorded a macro to do some work on any given line and we
want to repeat that macro n-times on contiguous lines. We have two ways of
doing that:

- Execute the macro in *series* such as `5@a`. This will queue 5 repititions of
  the macro in series starting at the current line and continues forward. The
  execution of the macro on the next line is dependent on the execution of the
  macro on the current line being successful. If it *fails* for any reason, the
  execution of the macro for the remaining lines will abort.
- Execute the macro in *parallel* such as `'<,>':normal @a`. This will queue up
  number of lines in the visual selection repititions of the macro in parallel.
  This means the execution of the macro on each line is independent of the
  execution on other lines. Therefore, even if one execution failed, the macro
  will still be applied to the remaining lines.

Which one to use depends on the use case. If we want the error to be obvious,
then execution in series is better.
