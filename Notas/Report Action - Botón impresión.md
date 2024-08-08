> [[Actions|Back]]

Tags: 
Status: 
Related: 

___

# Report Actions
Botones que nos permiten imprimir [[Reportes o Informes]]

> [!MODELO] 
> `ir.actions.report`

```xml
<record id="pnt_lot_picking_quality_control" model="ir.actions.report">
	# Nombre del reporte
	<field name="name">Picking Quality Control</field>
	# Modelo en el que se encuentra la accion
	<field name="model">mrp.production</field>
	# Tipo de reporte
	<field name="report_type">qweb-pdf</field>
	# Reporte al que llama
	<field name="report_name">report_pnt.pnt_report_mrp_quality_control</field>
	<field name="report_file">report_pnt.pnt_report_mrp_quality_control</field>
	# Nombre del reporte que se imprime
	<field name="print_report_name">'Picking Quality - %s' % (object.display_name)</field>
	<field name="binding_model_id" ref="mrp.model_mrp_production"/>
	<field name="binding_type">report</field>
	# Referencia del paperformat que se aplica
	<field name="paperformat_id" ref="report_pnt.paperformat_internal_pnt"/>
</record>
```

```xml
<record id="pnt_lot_picking_quality_control" model="ir.actions.report">  
    <field name="name">Picking Quality Control</field>  
    <field name="model">mrp.production</field>  
    <field name="report_type">qweb-pdf</field>  
    <field name="report_name">report_pnt.pnt_report_mrp_quality_control</field>  
    <field name="report_file">report_pnt.pnt_report_mrp_quality_control</field>  
    <field name="print_report_name">'Picking Quality - %s' % (object.display_name)  
    </field>  
    <field name="binding_model_id" ref="mrp.model_mrp_production"/>  
    <field name="binding_type">report</field>  
    <field name="paperformat_id" ref="report_pnt.paperformat_internal_pnt"/>  
</record>
```



# Añadir nuevo Report Action (imprimir reporte)
Queremos añadir un nuevo botón para imprimir un reporte como el que vemos a continuación:

![[Pasted image 20240108090828.png]]

## Ejemplo 1 

Impresión de documento xlsx.
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

Impresión de documento pdf.
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

