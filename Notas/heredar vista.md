> [[Heredar]]

Tags: 
Status: 
Related: 

___

# heredar vista

```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <record id="pnt_{{NAME_}}" model="ir.ui.view">  
        <field name="model">{{MODELO.}}</field>  
        <field name='inherit_id' ref='{{sale.view_order_form}}'/>  
        <field name="priority" eval="999"/>  
        <field name="arch" type="xml">  
            <xpath expr="//" position="after">  
            </xpath>  
        </field>  
    </record>  
</odoo>
```