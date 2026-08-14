#ruby #rails #decorators #draper #design-patterns #presentation

A decorator wraps a model to add view/presentation-only behavior, without polluting the model itself with formatting logic it has no business knowing about.

## Example (Draper-style)

[Draper](https://github.com/drapergem/draper) is the common gem for this, `delegate_all` forwards any unhandled method call to the wrapped object:

``` ruby
class OrderDecorator < Draper::Decorator
  delegate_all

  def formatted_total
    h.number_to_currency(total)
  end

  def status_badge_class
    paid? ? 'badge-success' : 'badge-warning'
  end
end

# In a view or controller:
order.decorate.formatted_total
```

`h` gives access to Rails view helpers (like `number_to_currency`) from inside the decorator.

## Anti-Patterns

- No business logic. `status_badge_class` mapping a status to a CSS class is presentation, deciding whether an order *can* be cancelled is business logic and belongs on the model or a service object.
- No database queries. A decorator formats what it's given, it doesn't go fetch more data, that keeps it cheap to instantiate and easy to test without a database.
- Don't decorate inside a model or service object. Decorators exist for the view layer, mixing them into business logic couples unrelated concerns together.
