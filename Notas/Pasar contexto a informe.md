> [[Back]]

Tags: 
Status: 
Related: 

___

# Pasar contexto a informe

> Para pasar contexto al boton de un informe

```xml
<field name="context">{'group_lines': True}</field>  
```

```xml
<record id="pnt_grouped_sale_order_ids" model="ir.actions.report">
    <field name="name">GSO</field>  
    <field name="model">sale.order</field>  
    <field name="report_type">qweb-pdf</field>  
    <field name="report_name">reports_pcv.pnt_grouped_tens</field>  
    <field name="report_file">reports_pcv.pnt_grouped_tens</field>  
    <field name="print_report_name">'TALYTAL'</field>  
    <field name="binding_model_id" ref="sale.model_sale_order"/>  
    <field name="binding_type">report</field>  
    <field name="context">{'group_lines': True}</field>  
</record>
```