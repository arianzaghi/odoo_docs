> [[Search View]]

Tags: 
Status: 
Related: 

___
# Filtros dinámicos Search View

![[Pasted image 20241212135235.png]]

> Como el campo es dinamico, no lo podemos buscar ni en el groupby ni en el filter. 
## En sale order

```xml
<record id="pnt_sale_order_tree_groupby" model="ir.ui.view">  
    <field name="name">pnt.sale.order.form</field>  
    <field name="model">sale.order</field>  
    <field name="inherit_id" ref="sale.view_sales_order_filter"/>  
    <field name="arch" type="xml">  
        <xpath expr="//search" position="inside">  
            <field string="Contact" name="pnt_contact"/>
        </xpath>  
    </field>  
</record>
```