> [[Odoo Modelos|Back]]

Tags: #modelo
Status: 
Related: 

___

# custom_pnt

> [!Crear nuevo módulo]
> Duplicamos `dev-tools/scaffolding/custom_pnt` en la carpera de nuestro cliente

> [!ERROR] IMPORTANTE
> Después de crear un nuevo módulo, es imprescindible instalarlo desde odoo
> 
> 	`Ajustes > Aplicaciones > custom_pnt > instalar`
## Modelos

Los modelos que se crean dentro de `custom_pnt` extienden clases existentes o crean nuevas y tienen como función ampliar o alterar el funcionamiento de las clases. 


### Ejemplo

> `pnt_mi_clase_nueva.py`

```python
from odoo import _, api, fields, models  
  
  
class MiClaseNueva(models.Model):
  
    pnt_variable_nueva = fields.Date(  
		string="Fecha acordada",  
    )
```

> `sale_order.py`

```python
from odoo import _, api, fields, models  
  
  
class SaleOrder(models.Model):  
    _inherit = "sale.order"  
  
    pnt_shipping_costs = fields.Monetary(  
        string="Shipping costs per kg",  
    )
```