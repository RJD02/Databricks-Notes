VACCUM removes all files from the table directory that are not managed by Delta, as well as data files that are no longer in the latest state of the transaction log for the table and are older than a retention threshold.

VACCUM will skip all directories that begin with an underscore(\_) which includes the `_delta_log`.

Partitioning our table on a column that begins with an underscore is an exception to this rule.

Delta table files are deleted according to the time they have been logically removed from Delta's transaction log plus retention hours, not their modification timestamps on the storage system. The default threshold is 7 days.

*Databricks doesn't automatically trigger VACCUM operations*

If we run VACCUM on a Delta table, we will lose the ability to [[time travel]] back to a version older than the specified data retention period.

# VACCUM a non-Delta table
Recursively vaccums directories associated with the non-Delta table and remove uncommited files older than a retention threshold.
On these type of tables, Databricks automatically triggers VACCUM operations as data is written.

