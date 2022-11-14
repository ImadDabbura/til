In big data frameworks such as `Hive` or `Spark`, you always hear that this table is a **managed table** and that is an **external table**. What is actually the difference:

- *Managed table* is a table that the framework manages both the metadata about the table and its data directories. So when we drop the managed table, both the metadata and the actual data directories will be deleted.
- *External table*, on the other hand, is a table where the framework maintains metadata about it w/o actually managing the data itself. Therefore, when we drop it, only the metadata is deleted but the data directories stay intact.
