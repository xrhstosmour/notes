#ruby #rspec #testing #tdd #factorybot

[RSpec](https://rspec.info/) is the dominant behavior-driven testing framework for Ruby.

## Structure

`describe` groups examples for a class/method, `context` groups examples by scenario/state, `it` is a single example:

``` ruby
RSpec.describe Order do
  describe '#total' do
    context 'when the order has line items' do
      it 'sums the line item amounts' do
        order = Order.new(line_items: [LineItem.new(amount: 10), LineItem.new(amount: 5)])

        expect(order.total).to eq(15)
      end
    end

    context 'when the order has no line items' do
      it 'returns zero' do
        expect(Order.new(line_items: []).total).to eq(0)
      end
    end
  end
end
```

## `let` vs `let!` vs `before`

`let` is lazy and memoized, it only runs when first referenced in an example. `let!` forces eager evaluation before each example, useful when a record needs to exist in the database for the example to find it (e.g. via a query), not just to be referenced directly:

``` ruby
RSpec.describe Order do
  let(:customer) { Customer.new(name: 'Jane') } # Only built if an example references `customer`.
  let!(:pending_order) { Order.create!(customer: customer, status: 'pending') } # Exists in the DB up front.

  it 'finds pending orders' do
    expect(Order.pending).to include(pending_order)
  end
end
```

Prefer `let`/`let!` over instance variables set in `before`, they read closer to the example and avoid accidental cross-example state.

## FactoryBot

`build` instantiates without saving, `create` persists. Use `build` unless the test needs the record to actually exist (e.g. to be found by a query):

``` ruby
RSpec.describe Order do
  it 'validates presence of a customer' do
    order = build(:order, customer: nil)

    expect(order).not_to be_valid
  end
end
```

Traits express variations without duplicating a factory:

``` ruby
FactoryBot.define do
  factory :order do
    status { 'pending' }

    trait :paid do
      status { 'paid' }
    end
  end
end

create(:order, :paid)
```

## Avoiding Brittle Specs

- Don't assert on an object's class (`expect(result).to be_a(Hash)`), assert on its actual behavior/content instead, class-checking breaks on any refactor that preserves behavior but changes the type.
- Don't duplicate the same literal value across multiple examples, extract it to a `let`, so a change to the input only needs one edit.
- Don't put setup logic inside `it`, keep `it` to the action and assertion, setup belongs in `let`/`before`.

## Red-Green-Refactor

Write a failing example first (red), write the minimum code to pass it (green), then improve the implementation with the test as a safety net (refactor). This keeps every line of production code justified by a test that would fail without it.
