> [[ORM Methods]]

Tags: 
Status: 
Related: 

___

# read_groups
## [[Campos % porcentaje en agrupaciones de pivot y list modificando read_group]]

https://github.com/puntsistemes/wasterent_odoo/blob/14.0/report_pnt/models/account_move.py

```python
def invoice_line_grouped(self):
	invoice_line_grouped_ids = self.env["account.move.line"].read_group(
		domain=[
			("pnt_is_child_line_related", "=", True),
			("move_id", "=", self.id),
		],
		fields=[
			"name",
			"quantity:sum",
			"price_subtotal:sum",
			"price_total:sum",
			"discount",
			"price_unit",
		],
		groupby=[
			"product_id",
			"price_unit",
			"discount",
		],
		lazy=False,
	)
	return invoice_line_grouped_ids
```

```python
self.env["account.analytic.line"].read_group(  
            domain=[  
                ("project_id.pnt_project_type", "in", ["ane", "ae"]),  
                ("employee_id", "=", self.pnt_employee_ids[0].id),  
                ("date", ">=", first_day),  
                ("date", "<=", last_day),  
            ],  
            fields=["unit_amount"],  
            groupby=["date:day"],  
            lazy=False,  
        )
```

## Extraer fecha del `read_groups`
> Por defecto, la fecha sale en formato string (`25 Jan 2024`) pero queremos verla en formato Date.

![[Pasted image 20250127132120.png]]
Así que lo cogeremos del diccionario dentro de `range`

```python
group.get('__range').get('pnt_date:day').get('from')
```
