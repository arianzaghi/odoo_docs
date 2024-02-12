> [[Campo Computed|Back]]

Tags: 
Status: 
Related: 

___

# Hacer campo compute modificable

## Ejemplo 1

[`stock.picking.py`(core)](https://github.com/OCA/OCB/blob/16.0/addons/delivery/models/stock_picking.py)

```python
@api.depends('move_line_ids.result_package_id',
			 'move_line_ids.result_package_id.shipping_weight',
			 'weight_bulk')

shipping_weight = fields.Float(
	   "Weight for Shipping",
	   compute='_compute_shipping_weight')

def _compute_shipping_weight(self):  
    for picking in self:    
        picking.shipping_weight = 
        picking.weight_bulk + 
        sum([
			pack.shipping_weight or 
			pack.weight 
			for pack in picking.package_ids])

```

### Redefinimos la clase y sustituimos el campo `shipping_weight` con las siguientes modificaciones
   
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


## Ejemplo 2

>[Disclima_47585](https://github.com/puntsistemes/distech_odoo/pull/9/commits/58fb1f3a798af4cd31405238f39104e13857a908#diff-8f4223269b93d45f51d8bdd02a0810cbc4668201ac204eae30e9e4a16447cabb)
>Si cambiamos `Fecha de entrega` manualmente, `Plazo de entrega` debe actualizarse para que ambos datos coincidan.
>
>- `Plazo de entrega` calcula el numero de días hasta la entrega
>- `Fecha de entrega` calcula la fecha usando el número de días que quedan


![[Pasted image 20240207090824.png]]

```python
class SaleOrderLine(models.Model):  
    _inherit = "sale.order.line"  
    
    pnt_delivery_date = fields.Date(  
        string="Delivery date",  
        help="Delivery date of the products to the customer",  
        compute="_compute_delivery_date",  
        store=False,  
        readonly=False,  
    )  
    
    @api.depends('customer_lead')  
    def _compute_delivery_date(self):  
        for line in self:  
            if line.customer_lead:  
                delta = timedelta(days=line.customer_lead)  
                line.pnt_delivery_date = datetime.now() + delta  
            else:  
                line.pnt_delivery_date = False  
                
    @api.depends('pnt_delivery_date')  
    def _compute_customer_lead(self):  
        super()._compute_customer_lead()  
        
        for line in self:  
            delta = timedelta(days=line.customer_lead)  
            fecha_supuesta = datetime.now() + delta  
            fecha_entrega = line.pnt_delivery_date  
            
            if fecha_entrega:  
                day_difference = (  
                        fecha_entrega - fecha_supuesta.date()).days  
            else:  
                day_difference = (  
                    datetime.now().date() - fecha_supuesta.date()).days  
                    
            if day_difference != 0:  
                line.customer_lead = float(day_difference)
```
