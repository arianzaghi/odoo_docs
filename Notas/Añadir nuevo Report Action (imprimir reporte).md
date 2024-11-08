> [[Report Action - Botón impresión]]

Tags: 
Status: 
Related: 

___

# Añadir nuevo Report Action (imprimir reporte)

> Queremos añadir un nuevo botón para imprimir un reporte como el que vemos a continuación:

![[Pasted image 20240108090828.png]]

## Ejemplo 1 
> Impresión de documento xlsx.
```python
<?xml version="1.0" encoding="UTF-8" ?>  
<odoo>  
    <record id="pnt_partner_medicine_action_report_xlsx" model="ir.actions.report">  
            <field name="name">Partner Medicine XLSX</field>  
            <field name="model">res.partner</field>  
            <field name="report_type">xlsx</field>  
            <field name="report_name">report_pnt.pnt_partner_medicine_report_xlsx</field>  
            <field name="report_file">report_pnt.pnt_partner_medicine_report_xlsx</field>  
            <field name="binding_model_id" ref="base.model_res_partner" />  
            <field name="binding_type">report</field>  
            <field name="print_report_name">(object._get_report_base_filename())</field>  
        </record>  
</odoo>
```

## Ejemplo 2
> Impresión de documento pdf.
```python
<record id="action_report_urban_structure_albaran" model="ir.actions.report">
    <field name="name">Albaran Urban</field>
    <field name="model">sale.order</field>
    <field name="report_type">qweb-pdf</field>
    <field name="report_name">report_pnt.report_urban_structure_albaran</field>
    <field name="binding_model_id" ref="model_sale_order"/>
    <field name="binding_type">report</field>
    <field name="paperformat_id" ref="report_pnt.paperformat_report_urban_structure"/>
</record>
```

