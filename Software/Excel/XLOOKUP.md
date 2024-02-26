#excel #xlookup

## How to Use `XLOOKUP` in Excel

The `XLOOKUP` function in Excel is a powerful tool for searching a range or an array, and returning an item corresponding to the first match it finds. If a match doesn't exist, it can return an optional default value. The function signature is as follows:

``` plaintext
XLOOKUP(lookup_value, lookup_array, return_array, [if_not_found], [match_mode], [search_mode])
```

### Parameters

- **lookup_value**: The value to search for.
- **lookup_array**: The array or range to search.
- **return_array**: The array or range from which to return a value.
- **if_not_found** (optional): The value to return if `lookup_value` is not found. This is optional.
- **match_mode** (optional): Specifies the match type. 0 for exact match (default), -1 for exact match or next smaller item, 1 for exact match or next larger item, and 2 for a wildcard match.
- **search_mode** (optional): Specifies the search mode. 1 for a search that starts at the first item (default), -1 for a search that starts at the last item, 2 for a binary search that finds an exact match, and -2 for a binary search that finds the closest match, assuming data is sorted.

### Example Usage

Consider you have a database of products in an Excel sheet named `on_database`, with SKUs listed in column A and the corresponding quantity in column F. You want to look up the quantity based on the SKU provided in another sheet or table cell. You can use `XLOOKUP` like this:

``` excel
=XLOOKUP([@[SKU]], on_database!A:A, on_database!F:F)
```

#### Explanation

- `[@[SKU]]`: This is the SKU you're looking up. Assuming this formula is used within a table, it refers to the current row's `SKU` value.
- `on_database!A:A`: The range where the SKU is searched. This is the entire column A in the `on_database` sheet.
- `on_database!F:F`: The range from which to return the quantity, corresponding to the found SKU. This is the entire column F in the `on_database` sheet.

This formula searches for the SKU in column A of the `on_database` sheet and returns the corresponding quantity from column F of the same sheet. If the SKU is not found, `XLOOKUP` will return an error unless an `if_not_found` argument is specified.

### Benefits of Using `XLOOKUP`

- **Simplicity**: Replaces older functions like `VLOOKUP`, `HLOOKUP`, and `LOOKUP` with a more straightforward syntax.
- **Flexibility**: Allows for reverse lookups and searches with different match modes.
- **Safety**: Returns an optional default value if the lookup value isn't found, avoiding potential errors in your data processing.

`XLOOKUP` significantly enhances Excel's lookup capabilities, making data retrieval tasks more efficient and less prone to error.
