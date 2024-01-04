> [[Back]]

Tags: 
Status: 
Related: 

___

# Actions - Botón Acción

````python
<record id="action_report_urban_structure_albaran" model="ir.actions.report">  
<field name="name">Albaran Urban</field>  
<field name="model">sale.order</field>  
<field name="report_type">qweb-pdf</field>  
<field name="report_name">report_pnt.report_urban_structure_albaran</field> 
<field name="binding_model_id" ref="model_sale_order"/>  
<field name="binding_type">report</field>  
<field name="paperformat_id" ref="report_pnt.paperformat_report_urban_structure"/>  
</record>
````