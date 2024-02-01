> [[Campos avanzados|Back]]

Tags: 
Status: 
Related: 

___

# fields.Selection

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

## Recuperar el valor en lugar de la clave
Útil cuando tenemos un selection y queremos mostrar la opción por pantalla o en un informe.
Asi podemos mostrar el valor (Mayor puntuación) en lugar de la clave (pnt_highest_score)

`dict(self_fields[nombre del campo], description_selection(self.env))).get(objeto_modelo_capo)`


### Ejemplos

### [[Selection de todos los idiomas]]
### [[Selection de idiomas activos]]