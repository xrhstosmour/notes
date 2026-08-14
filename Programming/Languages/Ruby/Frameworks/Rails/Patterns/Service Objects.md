#ruby #rails #service-objects #design-patterns #architecture

A service object extracts a single business operation out of a model or controller into its own class, useful once an action involves multiple steps, touches multiple models, or has enough branching to clutter a "fat model."

## Class-Method Factory

A `self.call` (or a domain-named class method) builds and delegates to an instance, so callers don't need to know about `.new` plus a separate call:

``` ruby
class OrderCreator
  def self.call(...)
    new(...).call
  end

  def initialize(customer:, line_items:)
    @customer = customer
    @line_items = line_items
  end

  def call
    Order.create!(customer: @customer, line_items: @line_items)
  end
end

OrderCreator.call(customer: customer, line_items: line_items)
```

## Result/Railway Pattern

When an operation can fail in an expected way (not an exception-worthy bug), returning a result object lets the caller branch on success/failure without `begin`/`rescue`:

``` ruby
class Result
  attr_reader :value, :error

  def self.success(value) = new(success: true, value: value)
  def self.failure(error) = new(success: false, error: error)

  def initialize(success:, value: nil, error: nil)
    @success = success
    @value = value
    @error = error
  end

  def success? = @success
  def failure? = !success?
end

class OrderCreator
  def self.call(...)
    new(...).call
  end

  def initialize(customer:, line_items:)
    @customer = customer
    @line_items = line_items
  end

  def call
    return Result.failure('customer required') if @customer.nil?

    order = Order.create!(customer: @customer, line_items: @line_items)
    Result.success(order)
  end
end

result = OrderCreator.call(customer: nil, line_items: [])
result.success? ? render(result.value) : render_error(result.error)
```

Keep the object doing one thing, if it grows a second unrelated responsibility, split it rather than adding more branches.
