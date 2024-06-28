> [[Back]]

Tags: 
Status: 
Related: 

___

# Agrupar lineas albaran por product_id y lot_id

> Para nuestro informe customizado, queremos mostrar una hoja por cada producto, pero agrupándolos por `product_id` y por `lot_id` de tal manera que si tenemos:

cheese, 50kg, lot: A78
cheese, 25kg, lot: A78
cheese, 100kg, lot: A80>

Estas 3 lineas se convierten en

cheese, 75kg, lot: A78
cheese, 100kg, lot: A80

## Programación
```python
def get_grouped_move_lines(self):  
    grouped_lines = {}  
    for line in self.move_line_ids:  
        key = (line.product_id.id, line.lot_id.id)  
        if key in grouped_lines:  
            grouped_lines[key]['qty_done'] += line.qty_done  
        else:  
            has_quality_point = self.pnt_find_product_quality_point(line.product_id.id)  
            if has_quality_point:  
                grouped_lines[key] = {  
                    'product_id': line.product_id,  
                    'product_uom_id': line.product_uom_id,  
                    'lot_id': line.lot_id,  
                    'move_id': line.move_id,  
                    'qty_done': line.qty_done,  
                }  
    return grouped_lines.values()
```