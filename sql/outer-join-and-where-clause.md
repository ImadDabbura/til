With an outer join such as `LEFT OUTER JOIN`, we typically want all the records from the left table and records from right table that satisfy the join condition. However, if we include any field from the right table in the `where` clause, the join becomes an `INNER JOIN` for the following reason:

- Records from the left table that don't find a match in the right table will have `NULL` values in the fields from the right table
- Comparing `NULL` to any value results in `NULL`
- Because `WHERE` only returns records that evaluate to `true` and discard records that evaluates to either `false` or `NULL`
- Therefore, records with `NULL` values will be excluded. This means only the join becomes `INNER JOIN`

The above works the same for any form of `OUTER JOIN`. 

To work around this, add the predicate to join statement after `ON` clause.
