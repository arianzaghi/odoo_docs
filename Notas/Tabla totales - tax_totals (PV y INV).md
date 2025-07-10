> [[025 - Informes XML]]

Tags: 
Status: 
Related: [[PV Tabla totales]]

___

# PV y INV - tax_totals

> [[PV Tabla totales]] se utiliza en Pedido de Venta y en Facturas.
![[Pasted image 20241203163813.png]]

> [!INFO] INFO
> La tabla recibe como parametro el campo `tax_totals` de `sale.order`. 
> - Es un diccionario de valores
> - Este es un campo de tipo compute que llama a `_prepare_tax_totals` en `account.tax`

### `Tabla totales`
```xml
<template id="stock_account_report_invoice_document" inherit_id="account.report_invoice_document">
```
### `sale.order`
```python
@api.depends_context('lang')  
@api.depends('order_line.tax_id', 'order_line.price_unit', 'amount_total', 'amount_untaxed', 'currency_id')  
def _compute_tax_totals(self):  
    for order in self:  
        order = order.with_company(order.company_id)  
        order_lines = order.order_line.filtered(lambda x: not x.display_type)  
        order.tax_totals = order.env['account.tax']._prepare_tax_totals(  
            [x._convert_to_tax_base_line_dict() for x in order_lines],  
            order.currency_id or order.company_id.currency_id,  
        )
```

### Cambiar datos de la tabla
> Queremos calcular los totales de lineas de varios pedidos. Utilizaremos el primer pedido como cabecera.

**Establecemos método que calcule datos de la nueva tabla**
```python
@api.model  
def _get_grouped_tax_totals(self, orders):  
    """Obtiene base imponible, iva y total de los pedidos seleccionados."""  
  
    order = self[0].with_company(self[0].company_id)  
    order_lines = self._get_grouped_orders(orders)  
    tax_totals = order.env['account.tax']._prepare_tax_totals(  
        [x._convert_to_tax_base_line_dict() for x in order_lines],  
        order.currency_id or order.company_id.currency_id,  
    )  
  
    return tax_totals
```

**Heredamos sale order y cambiamos el valor de `tax_totals`**
```xml
<xpath expr="//t[@t-call='sale.document_tax_totals']" position="before">  
    <t t-if="docids">  
        <t t-set="tax_totals" t-value="doc._get_grouped_tax_totals(docids)"/>  
    </t>  
    <t t-else="">  
        <t t-set="tax_totals" t-value="doc.tax_totals"/>  
    </t>
</xpath>
```

### Modificar decimales en Cantidad

![[Pasted image 20250613084307.png]]

```xml
<!-- Poner a 0 decimales de la tabla de lotes y numeros de serie -->  
<template id="pnt_stock_account_report_invoice_document" inherit_id="account.report_invoice_document">  
    <t t-esc="snln_line['quantity']" position="attributes">
	    <!-- Quitamos , y pasamos a float -->  
        <attribute name="t-esc">float(snln_line['quantity'].replace(',', '.'))</attribute>  
        <attribute name="t-options">{'widget': 'float', 'precision': 0}</attribute>  
    </t>  
</template>
```