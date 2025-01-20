> [[Pedido de Venta (PV)]]

Tags: 
Status: 
Related: [[Tabla totales - tax_totals (PV y INV)]]

___

# Imprimir varios PV en un solo informe con una cabecera

> Dado que tenemos varios PV para el mismo cliente y con la misma cuenta analítica, queremos imprimir todas las lineas de todos los pedidos en un único informe con una misma cabecera
![[Pasted image 20241203174101.png]]
## Python
```python
class SaleOrder(models.Model):  
  
    _inherit = "sale.order"  
  
    def check_orders_and_print(self):  
        orders = self.browse(self.ids)  
        if not check_grouped_saleorders(orders):  
            raise UserError(_("All orders must have the same partner and analytic account."))  
        else:  
            return self.env.ref("reports_pcv.pnt_grouped_sale_order_ids_action").report_action(orders)  
  
    @api.model  
    def _get_grouped_orders(self, docids):  
        """Agrupa las líneas de los pedidos seleccionados."""  
  
        lines = []  
        for order in docids:  
            lines += order.order_line  
        return lines  
  
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
  
    def _get_orger_names(self, orders):  
        """Obtiene los nombres de los pedidos seleccionados."""  
  
        return ', '.join([order.name for order in orders])
```

## Llamada Informe
> Template que llama al documento de impresión
```xml
<template id="pnt_grouped_orders">  
    <t t-call="web.html_container">  
        <t t-set="doc" t-value="docs[0]"/>  
        <t t-set="docids" t-value="docs"/>  
  
        <t t-call="sale.report_saleorder_document"  
           t-lang="doc.partner_id.lang"/>  
    </t>  
</template>
```

> Boton para imprimir el informe
```xml
<record id="pnt_grouped_sale_order_ids_action" model="ir.actions.report">  
    <field name="name">'Grouped Sale Orders - %s' % (object.display_name)</field>  
    <field name="model">sale.order</field>  
    <field name="report_type">qweb-pdf</field>  
    <field name="report_name">reports_pcv.pnt_grouped_orders</field>  
    <field name="report_file">reports_pcv.pnt_grouped_orders</field>  
    <field name="print_report_name">'Grouped Sale Orders - %s' % (object.display_name)</field>  
    <field name="binding_model_id" ref="sale.model_sale_order"/>  
    <field name="binding_type">report</field>  
</record>
```

## Modificaciones Informe
```xml
%% Cambiar nombre de la orden por el resto de nombres %%
<xpath expr="//span[@t-field='doc.name']" position="replace">  
    <t t-if="docids">  
        <t t-set="order_names" t-value="doc._get_orger_names(docids)"/>  
        <span t-esc="order_names"/>  
    </t>  
    <t t-else="">  
        <span t-field="doc.name">SO0000</span>  
    </t>  
</xpath>

%% Cambiar datos de la tabla de totales %%
<xpath expr="//t[@t-call='sale.document_tax_totals']" position="before">  
    <t t-if="docids">  
        <t t-set="tax_totals" t-value="doc._get_grouped_tax_totals(docids)"/>  
    </t>  
    <t t-else="">  
        <t t-set="tax_totals" t-value="doc.tax_totals"/>  
    </t>    
</xpath>

%% Cambiar lineas que se van a imprimir %%
<xpath expr="//t[@t-foreach='lines_to_report']" position="before">  
    <t t-if="docids">  
        <t t-set="lines_to_report" t-value="doc._get_grouped_orders(docids)"/>  
    </t>  
    <t t-else="">  
        <t t-set="lines_to_report" t-value="doc._get_order_lines_to_report()"/>  
    </t>  
</xpath>

```