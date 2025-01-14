> [[Filtros estaticos Search View]]

Tags: 
Status: 
Related: 

___

# Establecer filtro por defecto en la acción

```xml
<record id="pnt_sale_order_line_action" model="ir.actions.act_window">  
    <field name="name">Sale Order Line</field>  
    <field name="res_model">sale.order.line</field>  
    <field name="view_mode">tree,form,pivot</field>  
    <field name="search_view_id" ref="view_sales_order_line_filter_inherit"/>  # RELACIONAMOS CON EL SEARCH VIEW
    <field name="context">{'search_default_{{FILTER_NAME}}': 1}</field>  # ESTABLECEMOS EL FILTRO
    <field name="help" type="html">  
        <p class="o_view_nocontent_smiling_face">No items created.</p>  
    </field>  
</record>
```

