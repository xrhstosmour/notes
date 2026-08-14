#database #migrations

1. **Create the database migration**: `rails g migration <migration_name>`

2. **Apply the database migration**: `rails db:migrate`

3. Rollback the database migration: `rails db:rollback`

## `change` vs `up`/`down`

Most migrations only need `change`, Rails infers how to reverse it automatically (e.g. `add_column` reverses to `remove_column`):

``` ruby
class AddStatusToOrders < ActiveRecord::Migration[7.1]
  def change
    add_column :orders, :status, :string
  end
end
```

When a migration isn't automatically reversible (data changes, or irreversible schema changes), define `up` and `down` explicitly instead of `change`:

``` ruby
class BackfillOrderStatus < ActiveRecord::Migration[7.1]
  def up
    Order.where(status: nil).update_all(status: 'pending')
  end

  def down
    raise ActiveRecord::IrreversibleMigration
  end
end
```

## Adding a Column with an Index or Foreign Key

``` ruby
class AddCustomerToOrders < ActiveRecord::Migration[7.1]
  def change
    add_reference :orders, :customer, foreign_key: true, index: true
  end
end
```

## Safety Note: `NOT NULL` on Large Tables

Adding a `NOT NULL` column directly can lock a large table while every existing row is validated. Add the column nullable with a default first, backfill if needed, then add the `NOT NULL` constraint in a separate migration:

``` ruby
class AddStatusToOrders < ActiveRecord::Migration[7.1]
  def change
    add_column :orders, :status, :string, default: 'pending' # No NOT NULL yet.
  end
end

class MakeOrdersStatusRequired < ActiveRecord::Migration[7.1]
  def change
    change_column_null :orders, :status, false
  end
end
```
