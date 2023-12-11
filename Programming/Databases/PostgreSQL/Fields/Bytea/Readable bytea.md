#bytea #binary #utf8

To convert/select a bytea/binary field in a PostgreSQL database, in a readable format you can use the below query:
``` sql
SELECT convert_from(<bytea_field>, 'UTF8') FROM <table>;
```
