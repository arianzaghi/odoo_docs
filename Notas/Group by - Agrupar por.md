> [[Vista Form - Formulario|Back]]

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

```xml
<record id="pnt_view_daily_extra_hour_detail_search" model="ir.ui.view">  
    <field name="name">pnt.extra.hour.detail.search</field>  
    <field name="model">pnt.extra.hour.detail</field>  
    <field name="arch" type="xml">  
        <search string="Search Extra Hours Detail">  
  
            <!-- Group By Options -->  
            <group expand="1" string="Group By">  
                <filter string="Date" name="group_by_date" domain="[]" context="{'group_by':'pnt_date'}"/>  
                <filter string="Employee" name="group_by_employee" domain="[]"  
                        context="{'group_by':'pnt_employee_id'}"/>  
            </group>  
        </search>  
    </field>  
</record>
```