> [[Lista de informes XML]]

Tags: 
Status: 
Related: 

___

# Albaran (ALB)

**Nombre del informe original del CORE**
```xml
<template id="report_delivery_document">
```

**Tipo de operación:** `stock_picking.picking_type_id`
![[Pasted image 20240610130455.png]]

**Estado de la operación:**
- State != 'done'
	El informe usa `stock.move`
- State = 'done'
	El informe usa `stock.move.line`
> [Coralim v16](https://github.com/puntsistemes/coralim_odoo/pull/34)

## Modificaciones sobre el albarán
### [[Albaran Valorado]]
### [[Direcciones de entrega albaran]]
### [[Comprobar si es ALB de devolucion]]
### [[Cambiar de sitio direcciones del ALB]]

