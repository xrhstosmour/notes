#ruby #best-practices #style #rubocop #conventions

Style conventions that hold up in real, linted Ruby codebases (informed by common Rubocop rule sets), beyond the basics in [[Naming Conventions]].

## Predicate and Dangerous Method Suffixes

Methods that return a boolean end in `?`. Methods that mutate the receiver or otherwise behave more "dangerously" than their non-`!` counterpart end in `!`:

``` ruby
class Order
  def paid?
    status == 'paid'
  end

  def cancel!
    update!(status: 'cancelled')
  end
end
```

## Method Visibility

Group visibility modifiers rather than repeating them per method, and keep implementation details `private`:

``` ruby
class Invoice
  def total
    subtotal + tax
  end

  private

  def subtotal
    line_items.sum(&:amount)
  end

  def tax
    subtotal * TAX_RATE
  end
end
```

## Memoization

`@ivar ||= ...` is the standard memoization idiom, but it re-runs the computation every time if the result is `nil` or `false`. Guard with `defined?` when the computed value can legitimately be falsy:

``` ruby
class Report
  def summary
    @summary ||= build_summary # Fine when build_summary never returns nil/false.
  end

  def cached_result
    return @cached_result if defined?(@cached_result)

    @cached_result = expensive_lookup # Safe even if expensive_lookup returns nil/false.
  end
end
```

## Avoid Magic Numbers and Strings

Extract repeated literals into named constants, it documents intent and gives one place to change:

``` ruby
class Password
  MINIMUM_LENGTH = 8

  def valid?
    value.length >= MINIMUM_LENGTH
  end
end
```
