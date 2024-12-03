> [[Impresion de informes]]

Tags: 
Status: 
Related: 

___

# Imprimir informe desde un metodo o funcion python

> Queremos poder imprimir un informe desde un botón que no sea de tipo `report action`

```python
return self.env.ref("reports_pcv.pnt_grouped_sale_order_ids").report_action(self)
```
## Ejemplo

> Palacio v17 HU60709 - Imprimir varios informes juntos

**Boton para imprimir**
```xml
    <field name="name">sale.order.tree</field>  
    <field name="model">sale.order</field>  
    <field name="inherit_id" ref="sale.view_quotation_tree_with_onboarding"/>  
    <field name="arch" type="xml">  
        <tree position="inside">  
            <header>  
                <button name="check_orders_and_print" string="OCG" type="object"  
                        class="btn btn-primary"/>  
            </header>  
        </tree>  
    </field>  
</record>
```

**Metodo que imprime**
```python
def check_orders_and_print(self):  
    orders = self.browse(self.ids)  
    if not self.check_grouped_saleorders(orders):  
        raise UserError(_("XX All orders must have the same partner and analytic account."))  
    else:  
        return self.env.ref("reports_pcv.pnt_grouped_sale_order_ids").report_action(orders)
```

**Llamamos a esta accion para imprimir. La accion llama al template invocacion**
```xml
<template id="pnt_grouped_tens">  
    <t t-call="web.html_container">  
        <t t-set="doc" t-value="docs[0]"/>  
        <t t-set="doc_ids" t-value="docs"/>  
        <t t-call="sale.report_saleorder_document"  
           t-lang="doc.partner_id.lang"/>  
    </t>  
</template>

<record id="pnt_grouped_sale_order_ids" model="ir.actions.report">  
    <field name="name">GSO</field>  
    <field name="model">sale.order</field>  
    <field name="report_type">qweb-pdf</field>  
    <field name="report_name">reports_pcv.pnt_grouped_tens</field>  
    <field name="report_file">reports_pcv.pnt_grouped_tens</field>  
    <field name="print_report_name">'TALYTAL'</field>  
    <field name="binding_model_id" ref="sale.model_sale_order"/>  
    <field name="binding_type">report</field>  
</record>
```