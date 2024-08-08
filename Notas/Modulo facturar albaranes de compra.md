> [[Modulos custom de punt]]

Tags: 
Status: 
Related: 

___

# Modulo facturar albaranes de compra

[[Facturar albaranes esquema]]
## `purchase_picking_invoicer_pnt`

### Context prompt
```css
Review the following inheritance of the odoo v14 class `account.move`
It allows us to add a new 'supplier_id', which is a new model that associates with one2many stock pickings.
Uppon adding a new supplier_id to our invoice, the purchase order lines related to the lines on our supplier_id's pickings get transformed into invoice lines and added to our new invoice. Our invoice lines also receive as vals, the id of the picking where it comes from.
The pickings are that have been linked through a supplier_id are also kept on a one2many field (pnt_account_move_picking_ids) to see which pickings have been used.
```

### Proceso
1. Creamos pedido de compra y validamos
2. Creamos albarán o albaranes parciales y asignamos `picking_supplier_id`
3. Validamos los albaranes
4. Creamos devolución (total o parcial) de un albarán
5. Creamos nueva factura
6. Seleccionamos los `picking_supplier_id` y se cargan las lineas de factura correspondientes al albarán.

### Comportamiento esperado
- Las devoluciones no se ven reflejadas
- Al añadir un `picking_supplier_id`, no se vuelve a mostrar
- Al eliminar un `picking_supplier_id` del `many_2_many_tags`, se vuelve a mostrar
- Las lineas se mantienen individuales
- Las cantidades facturadas se muestran como `facturadas` en el Pedido de Compra

### Debug
```
update stock_picking set pnt_is_invoiced=false;
update pnt_stock_picking_supplier set pnt_all_invoiced=false;
```

## Version 1.0

> Se muestran los albaranes vinculados al `supplier_id` que se han cargado en esta factura

```python
def write(self, vals):  
    res = super(AccountMove, self).write(vals)  
    if 'pnt_loaded_picking_ids' in vals and 'pnt_history_picking_ids' not in vals:  
        self._delete_invoice_lines_if_picking_removed()  
    return res

def _delete_invoice_lines_if_picking_removed(self):  
    for record in self:  
        remaining_picking_ids = set(record.pnt_loaded_picking_ids.ids)  
        original_picking_ids = set(record.pnt_history_picking_ids.ids)  
        removed_picking_ids = original_picking_ids - remaining_picking_ids  
  
        if removed_picking_ids:  
            record._delete_invoice_lines_for_removed_pickings(removed_picking_ids)  
            record._sync_account_move_picking_ids()  
            record.env['stock.picking'].browse(list(removed_picking_ids)).write({'pnt_is_invoiced': False})

def _delete_invoice_lines_for_removed_pickings(self, removed_picking_ids):  
    lines_to_delete = self.env['account.move.line'].search([  
        ('move_id', '=', self.id),  
        ('pnt_stock_picking_ids', 'in', list(removed_picking_ids))  
    ])  
    lines_to_delete.unlink()


def _sync_account_move_picking_ids(self):  
    picking_ids = self.pnt_loaded_picking_ids.ids  
    self.write({  
        'pnt_history_supplier_ids': [(6, 0, picking_ids)]  
    })

@api.onchange("pnt_picking_supplier_id")  
def _onchange_pnt_picking_supplier_id(self):  
    if self.pnt_picking_supplier_id:  
  
        # ==== GET PICKINGS, MARK AS INVOICED AND ADD TO MANY2MANY ====  
        supplier_picking_ids = self.pnt_picking_supplier_id.pnt_picking_ids  
        if supplier_picking_ids.ids:  
            supplier_picking_ids.write({'pnt_is_invoiced': True})  
            self.write({  
                'pnt_loaded_picking_ids': [(4,  pid) for pid in supplier_picking_ids.ids],  
                'pnt_history_picking_ids': [(4, pid) for pid in supplier_picking_ids.ids],  
            })  
        # ====#
	...
```