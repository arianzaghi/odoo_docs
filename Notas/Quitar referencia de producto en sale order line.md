> [[sale.order.line]]

Tags: 
Status: 
Related: 

___

# Quitar referencia en las lineas de PV

> En el sale order line está el método _compute_name si le pasamos por contexto display_default_code=False Odoo te lo devuelve sin los corchetes.

```python
@api.depends("product_id")  
def _compute_name(self):  
    return super(  
        SaleOrderLine, self.with_context(display_default_code=False)  
    )._compute_name()
```