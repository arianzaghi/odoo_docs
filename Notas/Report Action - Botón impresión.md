> [[Actions]]

Tags: 
Status: 
Related: [[Estructura informes]]

___
# Report Actions
> Botones que nos permiten imprimir Informes

# [[Añadir nuevo Report Action (imprimir reporte)]]

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
