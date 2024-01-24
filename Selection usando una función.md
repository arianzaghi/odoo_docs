> [[fields.Selection|Back]]

Tags: 
Status: 
Related: [[fields.Selection]]

___

# Selection usando una función

> Campo selection usando una función

```python
from odoo import _, api, fields, models  
  
  
def _lang_get(self):  
    return self.env['res.lang'].get_installed()  
  
  
class ResPartner(models.Model):  
    _inherit = "res.partner"  
  
    pnt_documentation_lang = fields.Selection(  
        selection=_lang_get,  
        string='test',  
    )
```