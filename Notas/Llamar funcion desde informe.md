> [[Reportes o Informes]]

Tags: 
Status: 
Related: 

___

# Llamar funcion desde informe

## Vista
```xml
<div class="col-3 offset-5">  
    <strong>TOTAL NET WEIGHT:</strong>  
    <t t-set="total_delivered"  
       t-value="o._get_total_delivered()"/>  
    <span t-esc="total_delivered" t-options="{'widget': 'float', 'precision': 2}"/>  
    <span t-field="o.weight_uom_name"/>  
</div>
```

## Modelo
```python
def _get_total_delivered(self):  
    _sum = 0  
    for picking in self.move_line_ids:  
        _sum += picking.qty_done * picking.product_id.weight  
    return _sum
```