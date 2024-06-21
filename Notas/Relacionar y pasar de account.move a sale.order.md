> [[account.move]]

Tags: 
Status: 
Related: 

___

# Relacionar y pasar de account.move a sale.order

> No existe ningun campo `Many2one` que nos relacione desde `account_move` hasta `sale_order`


## Solución 1
> **Solución:** Creamos un campo compute que busque el pedido
```python
def _compute_repair_order_components(self):
    for move in self:
        related_orders = self.env['sale.order'].search([
            ('name', '=', move.invoice_origin)
        ]).campo_que_queremos
        move.campo_en_albaran = related_orders
```

## Solución 2
> Añadimos los campos en el create de la factura y en el método que llama al create

![[Pasted image 20240614110705.png]]
![[Pasted image 20240614110711.png]]