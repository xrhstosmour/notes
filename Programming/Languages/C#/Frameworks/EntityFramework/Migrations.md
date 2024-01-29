#database #migrations #snapshot

1. **Create the database migration:**

``` bash
dotnet ef migrations add <MigrationName>
```

2. **Apply the database migration:**

``` bash
dotnet ef database update
```
