> [[stock.picking]]

Tags:
Status:
Related:

---

# Vincular albaran con sale cuando hay entrega en 2 pasos

> Cuando la venta en dos pasos está activada, al confirmar una venta, se generan albaranes de PICK y de SALIDA.

> [!IMPORTANT] NOTA
> Únicamente el último albarán generado se relaciona con `sale.order.line`

### Solución 1

> Definimos un método que te obtenga la linea, para después poderla tratar nosotros

**Usando un método**

```python
# Metodo que devuelve la linea
def pnt_obtain_sale_order_line(self):
	if self.move_id.sale_line_id:
		return self.move_id.sale_line_id
	sale_line_ids = self.move_id.mapped("move_dest_ids.sale_line_id")
	if sale_line_ids:
		return sale_line_ids if len(sale_line_ids) == 1 else sale_line_ids[0]
	return False
```

**Usando compute**

```python
# Lo mismo pero con compute
@api.depends("move_id.move_dest_ids")  
def _compute_sale_order_line(self):  
    for line in self:  
        if line.move_id.sale_line_id:  
            line.pnt_sale_order_line = line.move_id.sale_line_id  
        sale_line_ids = line.move_id.mapped("move_dest_ids.sale_line_id")  
        if sale_line_ids:  
            line.pnt_sale_order_line = sale_line_ids if len(sale_line_ids) == 1 else sale_line_ids[0]  
        else:  
            line.pnt_sale_order_line = False
```

### Solución 2

> Como el objetivo es conseguir el numero de bultos (unidades/capacidad_paquete), en lugar de calcular este dato desde cada modelo que lo necesita, lo haremos directamente desde la clase `product.packaging` (clase común a varios modelos)

**Modificando el modelo** `product.packaging`

```python
from odoo import _, api, fields, models  
import math  
  
  
class ProductPackaging(models.Model):  
    _inherit = "product.packaging"  
  
    def pnt_calc_packaging_units(self, quantity):  
        return math.ceil(quantity/self.qty  
            if self.qty > 0  
            else 0  
        )
```

Cuando llamamos al método, aportamos el número de unidades y obtenemos el cálculo de bultos.

**Desde** `stock.move`

```python
class StockMove(models.Model):  
    _inherit = "stock.move"

	pnt_product_packaging_qty = fields.Integer(  
	    string="Number of packaging units",  
	    compute='_compute_product_packaging_qty',  
	)  
	  
	@api.depends("product_packaging_id")  
	def _compute_product_packaging_qty(self):  
	    for line in self:  
	        qty = line.quantity_done  
	        line.pnt_product_packaging_qty = line.product_packaging_id.pnt_calc_packaging_units(qty)
```

**Desde** `stock.move.line`

```python
class StockMoveLine(models.Model):  
    _inherit = "stock.move.line"
    
	pnt_product_packaging_qty = fields.Integer(  
	    string="Packaging Qty", compute="_compute_product_packaging_qty", readonly=True  
	)  
	  
	@api.depends("qty_done")  
	def _compute_product_packaging_qty(self):  
	    for line in self:  
	        qty = line.qty_done  
	        line.pnt_product_packaging_qty = line.move_id.product_packaging_id.pnt_calc_packaging_units(  
	            qty)
```

## Ejemplos

[Sarte v15](https://github.com/puntsistemes/sarte_odoo/blob/15.0/custom_pnt/models/stock_move.py#L68)
[Coralim v16](https://github.com/puntsistemes/coralim_odoo/pull/60/files#)