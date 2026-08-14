#database #sql #architecture

A relational database splits into two layers that are easy to conflate: the storage engine and the database management system (DBMS) around it. MySQL/MariaDB with InnoDB is a common example, InnoDB is the storage engine, MariaDB (or MySQL) is the DBMS that embeds it.

## Storage Engine (e.g. InnoDB)

- Physically stores and retrieves data on disk and in memory.
- Manages transactions (ACID guarantees).
- Handles concurrency control: row-level locking, multi-version concurrency control (MVCC).
- Owns indexing and the buffer pool/cache for frequently accessed pages.

## DBMS (e.g. MariaDB/MySQL)

- Parses incoming SQL and checks syntax.
- Optimizes the query, decides which indexes to use, join order, etc.
- Executes the query plan, calling into the storage engine whenever it needs to read or write data.
- Handles user authentication and permissions.
- Supports swapping storage engines (InnoDB, MyISAM, Aria, ...) for different workloads, since storage is decoupled from query processing.

## Why the split matters

A slow query is a DBMS-layer problem, a bad plan, a missing index, the optimizer not using an index that exists. A stuck transaction or lock contention is a storage-engine-layer problem. Knowing which layer owns which behavior narrows down where to look first.
