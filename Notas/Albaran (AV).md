> [[Lista de informes]]

Tags: 
Status: 
Related: 

___

# Albaran (AV)

**Nombre del informe:** `report_deliveryslip_document`

**Tipo de operación:** `stock_picking.picking_type_id`
![[Pasted image 20240610130455.png]]

**Estado de la operación:**
- State != 'done'
	El informe usa `stock.move`
- State = 'done'
	El informe usa `stock.move.line`
> [Coralim v16](https://github.com/puntsistemes/coralim_odoo/pull/34)

## Modificaciones sobre el albarán
### [[Albarán Valorado]]