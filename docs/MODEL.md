# Model and measure reference

Extracted from the current PBIX. Measure names below are the existing names, including spelling inconsistencies. Formulas are documented as found, not endorsed as validated results.

## Relationships

| From | To | Cardinality | Filter | Active |
| --- | --- | --- | --- | --- |
| Returns_1997-1998[product_id] | Products[product_id] | M:1 | Single | Yes |
| Transection[product_id] | Products[product_id] | M:1 | Single | Yes |
| Stores[region_id] | Regions[region_id] | M:1 | Single | Yes |
| Transection[transaction_date] | Calendar[date] | M:1 | Single | Yes |
| Transection[customer_id] | Customers[customer_id] | M:1 | Single | Yes |
| Transection[store_id] | Stores[store_id] | M:1 | Single | Yes |
| Returns_1997-1998[return_date] | Calendar[date] | M:1 | Single | Yes |
| Returns_1997-1998[store_id] | Stores[store_id] | M:1 | Single | Yes |
| Transection[stock_date] | Calendar[date] | M:1 | Single | No |

## Measures

### measure list · Total cost

```dax

SUMX(
    Transection,Transection[quantity] * RELATED(Products[product_cost]))
```

### measure list · profit

```dax

[Total Revenue] - [Total cost]
```

### measure list · Profit Margin

```dax

DIVIDE([profit],[Total Revenue])
```

### measure list · Total Returns

```dax

SUM('Returns_1997-1998'[quantity]
)
```

### measure list · Quantity Sold

```dax

SUM(Transection[quantity])
```

### measure list · Quantity Return

```dax
SUM(
    'Returns_1997-1998'[quantity])
```

### measure list · Return Rate

```dax

[Quantity Return] / [Quantity Sold]
```

### measure list · Total Orders

```dax
COUNTROWS(
    Transection)
```

### measure list · Total Revenue

```dax

SUMX(
    Transection,Transection[quantity] * RELATED(Products[Discount_Price]))
```

### measure list · Lm Transection

```dax

 CALCULATE(
    [Total Transectionn],
    DATEADD('Calendar'[date],
    -1,MONTH))
```

### measure list · Total Transectionn

```dax
COUNTROWS
(
     Transection)



```

### measure list · Lm Profit

```dax

CALCULATE(
    [profit],
    DATEADD('Calendar'[date],
    -1,MONTH))
```

### measure list · Lm Return

```dax
CALCULATE(
    [Total Returns],
    DATEADD('Calendar'[date],
    -1,MONTH))
```

### measure list · Lm Revenue

```dax
CALCULATE(
    [Total Revenue],
    DATEADD('Calendar'[date],
    -1,MONTH))
```

### measure list · Monthly Revenue Target

```dax

[Lm Revenue] * 1.05
```
