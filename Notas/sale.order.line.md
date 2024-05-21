> [[sale.order]]

Tags: #modelo
Status: 
Related: 

___

# sale.order.line

> Insertar campo en lineas de pedido.

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <record id="view_order_form" model="ir.ui.view">
        <field name="model">sale.order</field>
        <field name='inherit_id' ref='sale.view_order_form'/>
        <field name="priority" eval="999"/>
        <field name="arch" type="xml">
            <xpath expr="//field[@name='order_line']//tree//field[@name='price_unit']"
                   position="after">
                <field name="pnt_billing_date"/>
                <field name="pnt_accounting_entry_date"/>
                <field name="pnt_sale_tag"/>
            </xpath>
        </field>
    </record>
</odoo>
```