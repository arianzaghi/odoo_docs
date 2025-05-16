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
### [[Ocultar campo producto]]
### Tabla impuestos albaran (tabla inferior)
> `stock_picking_report_valued.valued_report_picking`


## Estructura de Albaran

La estructura del informe de albaranes en Odoo varía según el estado del albarán y las características de los productos involucrados (paquetes, números de serie o lotes).

Cuando el albarán **no está en estado "Hecho"**, se utiliza una tabla simple con tres columnas:
- Producto
- Ordenado
- Entregado

Esta estructura es uniforme, sin importar si el producto tiene número de serie, lote o paquete.

Una vez que el albarán **está en estado "Hecho"**, se utiliza una tabla más detallada, con columnas opcionales:
- Producto
- Ordenado *(solo si el producto no tiene número de serie)*
- Número de lote o serie *(solo si aplica)*
- Entregado

### Líneas de productos en albaranes hechos

Odoo determina el formato adecuado para cada línea del albarán dependiendo de dos factores: si la línea tiene **paquetes** asociados y si hay **número de serie o lote**.

- **Si la línea tiene paquetes**, se añade una fila que representa visualmente el nombre del paquete.
  - Si, además, el producto tiene número de serie o lote, se imprimen las líneas de producto individualmente, incluyendo el número correspondiente.
  - Si el producto **no tiene número de serie o lote**, las cantidades se agrupan por producto, mostrando totales por producto y omitiendo detalles individuales.

- **Si la línea no tiene paquetes**, se procede de forma similar:
  - Con número de serie o lote: se muestran líneas individuales por unidad.
  - Sin número de serie o lote: las líneas se agrupan por producto, mostrando cantidad total entregada y/o ordenada.

En un mismo albarán pueden convivir productos con y sin paquetes. Las líneas con paquetes siguen el esquema de agrupación y visualización por paquete, mientras que las demás se procesan con el sistema de agregación sin paquetes.

### Cantidades pendientes (backorders)

Las cantidades pendientes de entrega se calculan mediante la variable `backorders`. Esta identifica otros albaranes vinculados que aún no están completados ni cancelados. Si existen, se listan las cantidades pendientes para cada producto.

Esta lógica está centralizada en el método `_get_aggregated_product_quantities` del modelo `stock.move.line`. El método realiza lo siguiente:

1. Inicializa estructuras necesarias.
2. Detecta albaranes pendientes.
3. Itera sobre los movimientos de stock.
4. Agrupa por producto usando `aggregated_properties`.
5. Suma cantidades por producto.
6. Maneja movimientos sin líneas (por ejemplo, productos pedidos pero aún no registrados con detalle).
7. Devuelve un diccionario con productos y sus cantidades agregadas.

Este método ignora los lotes y números de serie, asumiendo que esos datos ya están correctamente desglosados en otras estructuras.

### Mostrar la descripción del pedido en el albarán

Es posible incluir la descripción del pedido en el informe del albarán, siempre que esta difiera del nombre del producto. Para ello se hereda del modelo `stock.rule` y se utiliza el campo `description_picking`. Este campo puede estar oculto en la vista del albarán y debe activarse manualmente. Empresas como Polivas, Coelbe y Towerdigital ya implementan este enfoque. La descripción se muestra como un `<p>` debajo del nombre del producto.

### Personalización: Agregar campos personalizados a las líneas agrupadas

Es posible añadir campos adicionales a las líneas agrupadas modificando el método `_get_aggregated_product_quantities` y ajustando el informe correspondiente. Aquí un ejemplo:

```python
def _get_aggregated_product_quantities(self, **kwargs):
    aggregated_move_lines = super()._get_aggregated_product_quantities(**kwargs)
    for move_line in self:
        line_key = self._get_aggregated_properties(move_line=move_line)["line_key"]
        pnt_product_intimoda_stock = move_line.pnt_product_intimoda_stock
        if line_key in aggregated_move_lines:
            aggregated_move_lines[line_key]["pnt_product_intimoda_stock"] = pnt_product_intimoda_stock
    return aggregated_move_lines
