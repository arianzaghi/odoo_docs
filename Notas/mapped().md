>[[ORM Methods|Back]]

Tags: #metodo
Status: 
Related: 

___
https://www.odoo.com/documentation/15.0/es/developer/reference/backend/orm.html?highlight=search#environment
# mapped()

### Definition

The `mapped()` method is an ORM function in Odoo designed to apply a specified function to all records within a given recordset.

### Syntax
```python
result = recordset.mapped(function)
```

### Example

```python
product_names_uppercase = 
	Product.search([]).mapped(lambda record: record.name.upper())

```