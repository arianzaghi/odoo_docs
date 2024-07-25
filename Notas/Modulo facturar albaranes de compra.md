> [[Back]]

Tags: 
Status: 
Related: 

___

# Modulo facturar albaranes de compra

## `po_picking_invoicing_pnt`

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

### Debug
```
update stock_picking set pnt_is_invoiced=false;
update pnt_stock_picking_supplier set pnt_all_invoiced=false;
```

