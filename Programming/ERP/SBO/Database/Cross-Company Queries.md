#erp #sbo #mssql #database #cross-company #permissions

SAP Business One creates one SQL Server login per company database, named like `B1_<random_string>_RO` (read-only) and `B1_<random_string>_RW` (read-write). By default each login can only see its own company's database. To run a query joining across multiple company databases (e.g. from a reporting tool connecting once), grant that login access to the other databases too:

1. In SQL Server Management Studio, expand **Security → Logins**, find the `B1_<hash>_RO` (or `_RW`) login for the company the query will connect as.
2. Open its properties → **User Mapping**.
3. Tick the additional company databases that need to be queried, and grant them the `db_datareader` role (`db_datawriter` too if writes are needed, rarely appropriate for a reporting login).
4. The login can now reference the other databases directly in a query, e.g. `SELECT * FROM [OtherCompanyDB].dbo.OITM`.

Keep this scoped to read-only reporting logins where possible, granting a live SBO client login cross-database write access is a good way to corrupt another company's data from the wrong session.
