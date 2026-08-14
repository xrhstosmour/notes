#erp #sbo #pricing #discounts #calculation

Three common ways multiple discounts or a lump-sum discount get applied to a price or an order:

## Sequential

Each discount is applied on top of the result of the previous one, not on the original amount:

```
result = original
result = result - result * discount_1%
result = result - result * discount_2%
```

Example: 100, with a 15% then a 10% discount: `100 → 85 → 76.5`.

## Cumulative

Discount rates are summed first, then applied once to the original amount:

```
combined_rate = discount_1% + discount_2%
result = original - original * combined_rate%
```

Example: 100, with 10% and 15% combined into 25%: `100 → 75`.

Sequential and cumulative give different results whenever there's more than one discount, sequential is always ≥ cumulative for the same rates (each successive discount in a sequential chain applies to an already-reduced amount).

## Proportional Line Discount Allocation

To split a single lump-sum discount (e.g. a documentwide discount amount) across multiple order lines proportionally to each line's share of the total:

```
line_share% = 100 * line_total / document_total
line_discount = lump_sum_discount * line_share%
```

Example: a 100 lump-sum discount across two lines totaling 50,000 and 200 (document total 50,200): the first line gets `100 * 50000/50200 ≈ 99.6%` of the total's proportional weight, so it absorbs about 99.6 of the 100 discount, and the second line absorbs the remaining ~0.4.
