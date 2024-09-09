> [[Back]]

Tags: 
Status: 
Related: 

___

# Redirigir desde un modelo a otro para ver registros enlazados

```python
from odoo import models, fields, api

class ModelOne(models.Model):
    _name = 'model.one'
    _description = 'Model 1'

    name = fields.Char(string='Name')
    one2many_field = fields.One2many('model.two', 'model_one_id', string='Related Model 2 Records')

    def action_view_model_two(self):
        self.ensure_one()
        return {
            'type': 'ir.actions.act_window',
            'name': 'Related Model 2 Records',
            'res_model': 'model.two',
            'view_mode': 'tree,form',
            'domain': [('id', 'in', self.one2many_field.ids)],
            'context': {'default_model_one_id': self.id},
        }
```

