The logical execution order of an SQL query is defined by the following sequences:

1. The `FROM` clause is first evaluated to get the output relation
2. Then `WHERE` predicate is applied to the records in the output relation. If `WHERE` is not present, the predicate is `True`
3. Records satisfies the `WHERE` clause then placed into groups according to the `GROUPBY` clause. If `GROUPBY` clause is not present, all records will be placed into one group
4. Then groups will filtered acoording to `HAVING` clause. If it is not present, the predicate is `True`
5. Then the `SELECT` clause uses the remaining groups to generate results and, if they exist, apply aggregate functions on the results
6. Generated results will be sorted according to `ORDER by` clause if it is present. Otherwise, the results will be displayed randomly
7. Finally, if `LIMIT` is present, display the number of records requested in the `LIMIT` clause
