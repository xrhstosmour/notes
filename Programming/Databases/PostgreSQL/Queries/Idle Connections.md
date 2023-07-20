#postgresql #iddle-connections #database
To find idle connections in a PostgreSQL database execute the bellow query:
``` sql
SELECT
    pg_terminate_backend(pid)
FROM
    pg_stat_activity
WHERE
    datname = '<database_name>'
    AND pid <> pg_backend_pid()
    AND state in ('idle');
```
