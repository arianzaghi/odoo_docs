> 

Tags: 
Status: 
Related: 

___

# Hacer campo compute modificable

[`stock.picking.py`(core)](https://github.com/OCA/OCB/blob/16.0/addons/delivery/models/stock_picking.py)

```python
@api.depends('move_line_ids.result_package_id',
			 'move_line_ids.result_package_id.shipping_weight',
			 'weight_bulk')  
def _compute_shipping_weight(self):  
    for picking in self:    
        picking.shipping_weight = 
        picking.weight_bulk + 
        sum([
			pack.shipping_weight or 
			pack.weight 
			for pack in picking.package_ids])

shipping_weight = fields.Float(
	   "Weight for Shipping",
	   compute='_compute_shipping_weight')
```

## 1 Redefinimos la clase y sustituimos el campo `shipping_weight` con las siguientes modificaciones
   
   - Añadimos `readonly=False` para hacer que el campo sea modificable
   - Añadimos `store=True` para poder guardar en base de datos un valor

```python
shipping_weight = fields.Float(
   "Weight for Shipping",
   compute='_compute_shipping_weight',
   store=True,
   readonly=False,
)
```