#sbo #erp #stock #quantity #on-hand #committed #ordered

Using the follow query we can calculate the stock, for all the items/inventory inside a warehouse:

``` sql
WITH BoMCTE AS (
    SELECT T1.Father AS Code,
        T0.TreeType AS Type,
        CAST(ROUND(T0.Qauntity, 0) AS INT) AS Quantity,
        T1.Code AS ItemCode,
        CAST(ROUND(T1.Quantity, 0) AS INT) AS ComponentQuantity
    FROM OITT T0
        INNER JOIN ITT1 T1 ON T0.Code = T1.Father
        LEFT JOIN OITM T2 ON T0.Code = T2.ItemCode
        LEFT JOIN OITM T3 ON T1.Code = T3.ItemCode
    WHERE T0.TreeType IN ('S', 'A')
),
StockCTE AS (
    SELECT T0.ItemCode,
        CASE
            WHEN T2.Code IS NOT NULL THEN 'True'
            ELSE 'False'
        END AS IsBoM,
        CAST(ROUND(SUM(ISNULL(T0.OnHand, 0)), 0) AS INT) AS OnHand,
        CAST(ROUND(SUM(ISNULL(T0.IsCommited, 0)), 0) AS INT) AS IsCommitted,
        CAST(ROUND(SUM(ISNULL(T0.OnOrder, 0)), 0) AS INT) AS OnOrder
    FROM OITW T0
        INNER JOIN OITM T1 ON T0.ItemCode = T1.ItemCode
        LEFT JOIN OITT T2 ON T1.ItemCode = T2.Code
    WHERE T1.validFor = 'Y'
        AND T0.WhsCode = '<warehouse_code>'
        AND T1.SellItem = 'Y'
    GROUP BY T0.ItemCode,
        T2.Code
),
BoMStockCTE AS (
    SELECT B.Code,
        MIN(
            CAST(ROUND(S.OnHand / B.ComponentQuantity, 0) AS INT)
        ) AS BoMStock,
        MIN(
            CAST(
                ROUND(S.IsCommitted / B.ComponentQuantity, 0) AS INT
            )
        ) AS BoMIsCommitted,
        MIN(
            CAST(ROUND(S.OnOrder / B.ComponentQuantity, 0) AS INT)
        ) AS BoMOnOrder
    FROM BoMCTE B
        INNER JOIN StockCTE S ON B.ItemCode = S.ItemCode
    GROUP BY B.Code
)
SELECT DISTINCT COALESCE(E.Code, S.ItemCode) AS ItemCode,
    CASE
        WHEN E.Code IS NOT NULL THEN E.BoMStock
        ELSE S.OnHand
    END AS OnHand,
    CASE
        WHEN E.Code IS NOT NULL THEN E.BoMIsCommitted
        ELSE S.IsCommitted
    END AS IsCommitted,
    CASE
        WHEN E.Code IS NOT NULL THEN E.BoMOnOrder
        ELSE S.OnOrder
    END AS OnOrder,
    CASE
        WHEN E.Code IS NOT NULL THEN 'True'
        ELSE 'False'
    END AS IsBoM,
    ISNULL(B.Type, '-') AS BoMType
FROM StockCTE S
    LEFT JOIN BoMStockCTE E ON S.ItemCode = E.Code
    LEFT JOIN BoMCTE B ON S.ItemCode = B.Code;
```
