> [[Back]]

Tags: 
Status: 
Related: 

___

# Buscar Encontrar modelo original

>`res_partner`

```python
class Partner(models.Model):  
    _description = 'Contact'  
    _inherit = ['format.address.mixin', 'avatar.mixin']  
    _name = "res.partner"  
    _order = "display_name ASC, id DESC"  
    _rec_names_search = ['display_name', 'email', 'ref', 'vat', 'company_registry']
```

Ctrl+F: `_name = "model.name"` 