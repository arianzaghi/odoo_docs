> [[Formularios|Back]]

Tags: #xml
Status: 
Related: 

___

# Group by - Agrupar por

Los añadimos en la vista `SearchView`. Utilizamos un campo dentro del context para realizar el filtro

````python
<filter 
	string="Grouping criteria"
	name="invoice_grouping_criteria"  
	domain="[]"  
	context="{'group_by': 'pnt_grouping_field'}"
/>
````

## Ejemplo

````python
<record id="pnt_sale_order_tree_groupby" model="ir.ui.view">  
    <field name="name">pnt.sale.order.form</field>  
    <field name="model">sale.order</field>  
    <field name="inherit_id" ref="sale.view_sales_order_filter"/>  
    <field name="arch" type="xml">  
        <xpath expr="//group" position="inside">  
            <filter 
	            string="Grouping criteria"
	            name="invoice_grouping_criteria" 
				domain="[]"  
				context="{'group_by': pnt_grouping_field'}"
			/>  
        </xpath>  
    </field>  
</record>
````
