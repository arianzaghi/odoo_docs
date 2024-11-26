> [[Pedido de Compra (PC)]]

Tags: 
Status: 
Related: 

___
# Agrupar lineas pedido de compra
> Método para agrupar todas las lineas de un pedido de compra por producto.

```python
class PurchaseOrder(models.Model):  
    _inherit = "purchase.order"

def group_order_lines(self):  
    for order in self:  
        product_lines_map = {}  
        for line in order.order_line:  
            product_lines_map.setdefault(line.product_id, []).append(line)  
  
        for lines in product_lines_map.values():  
            if len(lines) > 1:  
                main_line = lines[0]  
                main_line.product_qty = sum(line.product_qty for line in lines)  
                for line in lines[1:]:  
                    line.unlink()
```

