> [[Informes XML]]

Tags: 
Status: 
Related: [[Albaran (AV)]] [[Pedido de Venta]]

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