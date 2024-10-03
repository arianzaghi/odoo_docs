[[Python framework|Back]]

Tags: #todo 
Status: 
Related: 

___

# ORM Methods

[[python orm create]]

## Search/Read
- `Model.browse([ids])`
	[[model.browse()]]
- [[Search domains]]

- [[self.ensure_one()]]
- [[mapped()]]
- [[search_count()]]


In Odoo, the `sale.order` model has a one-to-many relationship with its lines, typically defined as `order_line`. You can access all lines of a specific sale order using this field.

If you want a single line method to get all lines of a sale order, you can use the `mapped` function on the `order_line` field. Here's how you can do it:

1. **Ensure you have a sale order record.** For example, assume `sale_order` is the sale order record you are working with.
2. **Use the `mapped` function** to get a list of sale order lines.

The expression to use in PyCharm's "Evaluate Expression" option would look like this:

```python
sale_order.order_line.mapped('id')
```

This will return a list of IDs of the sale order lines. If you need more details about each line, you can map any other field or access the whole record. For instance:

- **To get all fields of the sale order lines:**

```python
sale_order.order_line
```

- **To get specific fields (e.g., product names):**

```python
sale_order.order_line.mapped('product_id.name')
```

### Example Expression for PyCharm's "Evaluate Expression"

Assuming `sale_order` is your active `sale.order` record:

- **To get the list of sale order line records:**

```python
sale_order.order_line
```

- **To get the names of products in the sale order lines:**

```python
sale_order.order_line.mapped('product_id.name')
```

### Example Usage in Code

Here's an example that you might run in an Odoo environment:

```python
sale_order = self.env['sale.order'].browse(1)  # Replace 1 with the actual sale order ID
order_lines = sale_order.order_line
for line in order_lines:
    print(line.product_id.name)
```

This approach is flexible and can be adapted depending on what specific information you need from the sale order lines.