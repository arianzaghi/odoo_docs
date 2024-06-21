> [[sale.order.line]]

Tags: 
Status: 
Related: 

___

# Modelo de Sale order lines, todos los registros

> Este modelo `sale-workflow/sale_order_line_input/` no está migrado a la v17
> Nos muestra todas las lineas de todos los pedidos de compra en un listado TREE que es editable.

![[Pasted image 20240611130130.png]]

## XML
```xml
<?xml version="1.0" ?>  
<odoo>  
    <record id="pnt_sale_order_line_tree_view" model="ir.ui.view">  
        <field name="name">sale.order.line.input.tree.</field>  
        <field name="model">sale.order.line</field>  
        <field name="priority">30</field>  
        <field name="arch" type="xml">  
            <tree create="false" editable="top">  
                <field name="order_id"/>  
                <field name="company_id"/>  
                <field name="order_partner_id"/>  
                <field name="product_id"/>  
                <field name="name"/>  
                <field name="product_uom_qty"/>  
                <field name="customer_lead"/>  
                <field name="price_unit"/>  
                <field name="pnt_billing_date"/>  
                <field name="pnt_accounting_entry_date"/>  
                <field name="pnt_sale_tag"/>  
                <field name="tax_id"/>  
                <field name="discount"/>  
                <field name="price_subtotal"/>  
            </tree>  
        </field>  
    </record>  
  
    <record id="pnt_sale_order_line_tree_action" model="ir.actions.act_window">  
        <field name="name">Sales Order Lines</field>  
        <field name="type">ir.actions.act_window</field>  
        <field name="res_model">sale.order.line</field>  
        <field name="view_mode">tree,form,pivot,graph</field>  
        <field name="view_id" ref="pnt_sale_order_line_tree_view" />  
    </record>  
    <menuitem  
        id="menu_sales_order_line_input"  
        action="pnt_sale_order_line_tree_action"  
        parent="sale.sale_order_menu"  
        sequence="50"  
    />  
</odoo>
```