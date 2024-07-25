
> [[Back]]

Tags: 
Status: 
Related: 

___

# Mostrar linea a linea resultados búsqueda multiple

> Obtenemos en una búsqueda un resultado de múltiples registros y queremos poder ver linea a linea los registros

![[Pasted image 20240712135305.png]]

```python
[(x, x.product_id, x.product_id.name) for x in self.purchase_id.order_line if x.comment_ids]
```

self.purchase_id.order_line.filtered(lambda x: x.id in purchase_line_ids)
```
[(x.id) for x in self.purchase_id.order_line.purchase_line_ids]
```

self.invoice_line_ids.filtered(lambda x: x.purchase_line_id.id in original_po_lines.ids)
```
[(x if x.purchase_line_id.id in original_po_lines.ids) for x in self.invoice_line_ids]
```

```python
self.pnt_picking_supplier_id.mapped(  
                'pnt_picking_ids.move_ids_without_package.purchase_line_id').ids
```