#sbo #erp #price #price-list
Using the follow query we can get the price, for all the items/inventory inside a warehouse:

``` sql
SELECT T0.ItemCode,
    COALESCE(T6.UomEntry, T1.UomEntry, '-1') AS UoMEntry,
    COALESCE(T6.UomCode, T1.UomCode, 'Base') AS UoMCode,
    T7.WhsCode AS WarehouseCode,
    COALESCE(T4.ListNum, T5.ListNum) AS PriceListID,
    COALESCE(T4.ListName, T5.ListName) AS PriceListName,
    COALESCE(T3.Price, T2.Price) AS Price,
    COALESCE(
        T3.Currency,
        T2.Currency,
        T4.PrimCurr,
        T5.PrimCurr
    ) AS Currency,
    COALESCE(T3.UpdateDate, T0.UpdateDate) AS UpdateDate,
    T0.UpdateTS
FROM OITM T0
    LEFT JOIN OUOM T1 ON T1.UomCode = T0.SalUnitMsr
    LEFT JOIN ITM1 T2 ON T2.ItemCode = T0.ItemCode
    AND T2.Price > 0
    LEFT JOIN ITM9 T3 ON T3.ItemCode = T0.ItemCode
    AND T3.Price > 0
    LEFT JOIN OPLN T4 ON T4.ListNum = T2.PriceList
    LEFT JOIN OPLN T5 ON T5.ListNum = T3.PriceList
    LEFT JOIN OUOM T6 ON T6.UomEntry = T3.UomEntry
    INNER JOIN OITW T7 ON T7.ItemCode = T0.ItemCode
WHERE (
        T3.Price > 0
        OR T2.Price > 0
    )
    AND T7.WhsCode = '<warehouse_code>';
```
