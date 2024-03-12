#sbo #erp #price #price-list
Using the follow query we can get the price, for all the items/inventory:

``` sql
SELECT T0.ItemCode AS item_code,
    COALESCE(T0.UomEntry, '-1') AS uom_entry,
    COALESCE(T1.UomCode, 'Base') AS uom_code,
    T1.UomName AS uom_name,
    T0.PriceList AS pricelist_code,
    T2.ListName AS pricelist_name,
    T0.Price AS price,
    COALESCE(
        T0.Currency,
        T2.PrimCurr,
        T2.AddCurr1,
        T2.AddCurr2
    ) AS currency,
    T0.PriceType AS price_type,
    T3.UpdateDate AS update_date
FROM ITM1 T0
    INNER JOIN OUOM T1 ON T1.UomEntry = T0.UomEntry
    INNER JOIN OPLN T2 ON T2.ListNum = T0.PriceList
    INNER JOIN OITM T3 ON T3.ItemCode = T0.ItemCode
UNION
SELECT T0.ItemCode AS item_code,
    COALESCE(T0.UomEntry, '-1') AS uom_entry,
    COALESCE(T1.UomCode, 'Base') AS uom_code,
    T1.UomName AS uom_name,
    T0.PriceList AS pricelist_code,
    T2.ListName AS pricelist_name,
    T0.Price AS price,
    COALESCE(
        T0.Currency,
        T2.PrimCurr,
        T2.AddCurr1,
        T2.AddCurr2
    ) AS currency,
    T0.PriceType AS price_type,
    T3.UpdateDate AS update_date
FROM ITM9 T0
    INNER JOIN OUOM T1 ON T1.UomEntry = T0.UomEntry
    INNER JOIN OPLN T2 ON T2.ListNum = T0.PriceList
    INNER JOIN OITM T3 ON T3.ItemCode = T0.ItemCode;
```
