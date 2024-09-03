> [[One2many|Back]]

Tags: 
Status: 
Related: 

___

# Inverse Field

En Odoo, el atributo `inverse_field` se utiliza en campos relacionales para especificar la relación inversa en un modelo relacionado. Este atributo es especialmente relevante en campos `one2many` y `many2many` y se refiere al campo en el modelo relacionado que establece la conexión de vuelta al modelo actual.

## Parent
```python
from odoo import models, fields

class ParentModel(models.Model):
    _name = 'parent.model'
    _description = 'Parent Model'

    # One2many field to reference child models
    child_ids = fields.One2many(
        comodel_name='child.model',  # Name of the child model
        inverse_name='parent_id',    # Name of the Many2one field in the child model
        string='Children'
    )
```

## Child
```python
from odoo import models, fields

class ChildModel(models.Model):
    _name = 'child.model'
    _description = 'Child Model'

    # Many2one field to reference the parent model
    parent_id = fields.Many2one(
        comodel_name='parent.model',  # Name of the parent model
        string='Parent',
        ondelete='cascade',  # Optional: to delete children if the parent is deleted
    )
```