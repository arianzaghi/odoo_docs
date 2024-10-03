> [[Albaran (ALB)]]

Tags: 
Status: 
Related: 

___

# Ver si es ALB de devolucion

1. Damos de alta campo nuevo en `tipos de operaciones`
2. Comprobamos si el bool está activo para ver si es una devolucion

`Campo bool`
```python
from odoo import models, fields, api, _  
  
  
class StockPickingType(models.Model):
    _inherit = "stock.picking.type"  
  
    pnt_is_return_type = fields.Boolean(  
        string="Operation of return type",  
        default=False,  
    )
```

`If bool activo`
```python
<t  t-set="address" position="attributes">  
     <attribute name="t-if">not o.picking_type_id.pnt_is_return_type</attribute>  
</t>
```