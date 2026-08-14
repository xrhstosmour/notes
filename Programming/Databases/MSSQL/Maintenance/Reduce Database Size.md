#mssql #database #maintenance #shrink

In SQL Server Management Studio, to reclaim space from an oversized transaction log:

1. Set the database's Recovery model to **Simple** (Database → Properties → Options), this breaks the log backup chain, only do this if point-in-time recovery isn't needed.
2. Right-click the database → **Tasks → Shrink → Files**, set File type to **Log**, and shrink.

Shrinking regularly is generally discouraged (it fragments indexes and the file just grows again), this is for reclaiming space after a one-off event that bloated the log, not a routine maintenance task.
