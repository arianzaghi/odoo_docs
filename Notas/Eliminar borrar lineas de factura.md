> [[account.move.line]]

Tags: 
Status: 
Related: 

___

# Eliminar borrar lineas de factura

> Para eliminar las lineas de las facturas, debe haber paridad con las lineas de los apuntes contables.

> [!INFO] Lineas de apuntes contables
> Son de tipo `account.move.line` igual que las lineas de factura.
> Siempre contienen 2 lineas adicionales a las lineas de factura:
> - Total de impuestos
> - Total base imponible
>   
> Estas dos lineas adicionales son las que deben de actualizarse acorde con las lineas de la factura para evitar el siguiente error:
> ![[Pasted image 20240806113329.png]]


### `delete_invoice_line_ids`
```python
def _delete_invoice_lines_for_removed_supplier_ids(self, removed_supplier_ids):  
  
    lines_to_delete = self.env['account.move.line'].search([  
        ('move_id', '=', self.id),  
        ('pnt_picking_supplier_id', 'in', list(removed_supplier_ids))  
    ])  
  
    lines_not_to_delete = self.env['account.move.line'].search([  
        ('move_id', '=', self.id),  
    ]) - lines_to_delete  
  
    arr = []  
    for line in lines_not_to_delete:  
        arr.append((4, line.id, False))  
    for line in lines_to_delete:  
        arr.append((2, line.id, False))  
  
    self.write({'invoice_line_ids': arr})
```