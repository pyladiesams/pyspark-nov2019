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

### Exercise 1.1

```python
def get_cents(dataframe):
  return dataframe.selectExpr("order_id", "unit_price * 100 as unit_price_cents")

display(get_cents(sales_dataframe))
```

### Exercise 2

``` 
low_cost_dataframe = sales_dataframe.filter("unit_cost * 2 <= unit_price")
```

## Exercise 2.2

```python
low_cost_5_rows = low_cost_dataframe.take(5)

for row in low_cost_5_rows:
  print(row)
```

### Exercise 3

``` 
average_unit_price_dataframe = sales_dataframe.groupBy('item_type').avg('unit_price')
```

## Exercise 3.3

```python
df_list = [cents_dataframe, low_cost_dataframe, average_unit_price_dataframe]

for df in df_list:
  print (df.count())
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

### Bonus challenge 3

```
from pyspark.sql.functions import udf
from random import randint

@udf('double')
def add_random(profit):
  random_number = randint(0, 100)
  return profit + random_number

display(sales_dataframe.withColumn('random_profit', add_random(sales_dataframe.total_profit)))
```