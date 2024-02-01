> [[Propiedades de campos|Back]]

Tags: 
Status: 
Related: [[@api.depends]]

___

# Computed field

To create a computed field, create a field and set its attribute `compute` to the name of a method. The computation method should set the value of the computed field for every record in `self`

```python
from odoo import api
total = fields.Float(compute='_compute_total')

@api.depends('value', 'tax')
def _compute_total(self):
    for record in self:
        record.total = record.value + record.value * record.tax
```

- Dependencies can be dotted paths when using sub-fields:

```python
@api.depends('line_ids.value')
def _compute_total(self):
    for record in self:
        record.total = sum(line.value for line in record.line_ids)
```

- computed fields are not stored by default, they are computed and returned when requested. Setting `store=True` will store them in the database and automatically enable searching.

- searching on a computed field can also be enabled by setting the `search` parameter. The value is a method name returning a [Search domains](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/orm.html#reference-orm-domains).

```python
upper_name = field.Char(compute='_compute_upper', search='_search_upper')

def _search_upper(self, operator, value):
    if operator == 'like':
        operator = 'ilike'
    return [('name', operator, value)]
```

- The search method is invoked when processing domains before doing an actual search on the model. It must return a domain equivalent to the condition: `field operator value`.
    

- Computed fields are readonly by default. To allow _setting_ values on a computed field, use the `inverse` parameter. It is the name of a function reversing the computation and setting the relevant fields:


```python
document = fields.Char(compute='_get_document', inverse='_set_document')

def _get_document(self):
    for record in self:
        with open(record.get_document_path) as f:
            record.document = f.read()
def _set_document(self):
    for record in self:
        if not record.document: continue
        with open(record.get_document_path()) as f:
            f.write(record.document)
```

multiple fields can be computed at the same time by the same method, just use the same method on all fields and set all of them:

```python
discount_value = fields.Float(compute='_apply_discount')
total = fields.Float(compute='_apply_discount')

@api.depends('value', 'discount')
def _apply_discount(self):
    for record in self:
        # compute actual discount from discount percentage
        discount = record.value * record.discount
        record.discount_value = discount
        record.total = record.value - discount
```