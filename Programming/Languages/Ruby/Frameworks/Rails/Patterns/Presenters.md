#ruby #rails #presenters #design-patterns #presentation

A presenter is a plain Ruby object that sits between a controller/view and the model, formatting data for display without adding logic to the model or the view. Unlike [[Decorators]], a presenter doesn't wrap a single model instance, it can combine data from several models or from the request itself.

``` ruby
class OrderSummaryPresenter
  def initialize(order, current_user)
    @order = order
    @current_user = current_user
  end

  def can_cancel?
    @order.pending? && @order.customer == @current_user
  end

  def total_with_currency
    "#{@order.total} #{@order.currency}"
  end
end

# In a controller or view:
OrderSummaryPresenter.new(order, current_user).total_with_currency
```

Use a presenter to:

- Keep `ActiveRecord` queries and business logic out of the view.
- Combine or reshape data from multiple models for a single screen.
- Share formatting logic across views without reaching for a helper.

Prefer a presenter over a view helper when the logic needs state (multiple inputs, not just formatting one value). Helpers are hard to test in isolation and share one global namespace across the whole app.
