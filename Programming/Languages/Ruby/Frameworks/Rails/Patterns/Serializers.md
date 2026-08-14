#ruby #rails #serializers #design-patterns #api

A serializer converts a model (or a collection of models) into the format sent over the wire, typically JSON. It owns the mapping from internal attributes to the public API shape, including which fields are exposed and how associations are represented.

``` ruby
class OrderSerializer
  def initialize(order, current_user)
    @order = order
    @current_user = current_user
  end

  def as_json
    {
      id: @order.id,
      total: @order.total,
      # Only expose internal notes to the order's own customer.
      internal_notes: (@order.notes if @current_user == @order.customer)
    }
  end
end
```

Use a serializer to:

- Keep the public API contract in one place, independent of the model's actual columns.
- Filter sensitive fields based on who's asking, a serializer can know about the current user, a model shouldn't.
- Decide how associations are represented, embedded inline vs. referenced by ID, without that decision leaking into controllers.

Caching a serialized response per-element, rather than per whole collection, avoids invalidating an entire cached list when only one record in it changes.
