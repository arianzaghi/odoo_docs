> [[Albaran (ALB)]]

Tags: 
Status: 
Related: [[Pedido de Venta (PV)]]

___

# Pasar descripcion Pedido Venta a Albaran


```python
from odoo import models  
  

class StockRule(models.Model):  
    _inherit = "stock.rule"  
  
    def _get_stock_move_values(self, product_id, product_qty, product_uom, location_id, name, origin, company_id, values):  
        res = super()._get_stock_move_values(product_id, product_qty, product_uom, location_id, name, origin, company_id, values)  
        if res.get("sale_line_id", False):  
            sale_line = self.env["sale.order.line"].browse(res.get("sale_line_id"))  
            res["description_picking"] = sale_line.name  
        return res
```

## Ejemplos

### [Mantra Miquel](https://github.com/puntsistemes/mantra-iluminacion_odoo/commit/758ebd8c6502360aac4eecd29db744522cbbc864)
### Usisa HU56363

#### `stock.move`
```python
from odoo import models, fields, api, _  
  
class StockMove(models.Model):  
    _inherit = "stock.move"  
  
    def _prepare_move_line_vals(self, quantity=None, reserved_quant=None):  
        res = super()._prepare_move_line_vals(  
            quantity=quantity, reserved_quant=reserved_quant  
        )  
        if res.get("move_id", False):  
            move = self.env["stock.move"].browse(res.get("move_id", False))  
            if move:  
                res.update({"pnt_description": move.description_picking})  
        return res  
  
    def _get_new_picking_values(self):  
        vals = super()._get_new_picking_values()  
        sale_note = self.sale_line_id.name  
        if sale_note:  
            vals['note'] = sale_note  
        return vals  
  
```

#### `stock.rule`
```python
class StockRule(models.Model):  
    _inherit = "stock.rule"  
  
    def _get_stock_move_values(  
            self,  
            product_id,  
            product_qty,  
            product_uom,  
            location_id,  
            name,  
            origin,  
            company_id,  
            values,  
    ):  
        res = super(StockRule, self)._get_stock_move_values(  
            product_id,  
            product_qty,  
            product_uom,  
            location_id,  
            name,  
            origin,  
            company_id,  
            values,  
        )  
        if values.get("sale_line_id", False):  
            sale = self.env['sale.order.line'].browse(  
                values.get('sale_line_id')) 
            res["description_picking"] = sale.name  
  
        return res
```
