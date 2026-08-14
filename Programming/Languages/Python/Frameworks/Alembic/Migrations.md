#python #alembic #sqlalchemy #database #migrations

[Alembic](https://alembic.sqlalchemy.org/) is the migration tool for SQLAlchemy.

1. Initialize (once per project):
```
poetry run alembic init alembic
```
2. Point `alembic/env.py` at the app's SQLAlchemy `Base.metadata` and database URL, so autogenerate can diff against the actual models.
3. Create the database, user, and any custom functions/extensions the schema needs before the first migration, Alembic manages schema changes, not the database's existence.
4. If the database already has the target schema and migrations are being introduced retroactively, mark it as up to date without running anything:
```
poetry run alembic stamp head
```
5. Generate a migration from model changes:
```
poetry run alembic revision --autogenerate -m "<description>"
```
Always review the generated migration, autogenerate misses some changes (e.g. table/column renames look like a drop + add).
6. Apply migrations:
```
poetry run alembic upgrade head
```
