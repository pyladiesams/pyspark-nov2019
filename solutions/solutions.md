# Solutions

... cheating, huh? It's ok, but try to ask someone around you before checking this file. I'm sure they'll be much nicer than a talking .md file.

### Warm-up exercise

```
id_date_dataframe = sales_dataframe.select('order_id', 'order_date')
```

### Exercise 1

``` 
cents_dataframe = sales_dataframe.selectExpr("order_id", "unit_price * 100 as unit_price_cents")
```

### Exercise 2

``` 
low_cost_dataframe = sales_dataframe.filter("unit_cost * 2 <= unit_price")
```

### Exercise 3

``` 
average_unit_price_dataframe = sales_dataframe.groupBy('item_type').avg('unit_price')
```

### Exercise 4

```sql
select item_type, sum(units_sold) from sales group by item_type
```

### Bonus challenge 1

``` 
units_per_type = sales_dataframe.groupBy('item_type').sum('units_sold')
```

### Bonus challenge 2

```
from random import randint

random_number = randint(0, 100)

more_profit_dataframe = sales_dataframe.selectExpr("order_id","total_profit as original_profit","total_profit + {} as modified_profit".format(str(random_number)))
```