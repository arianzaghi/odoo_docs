> [[List o Tree]]

Tags: 
Status: 
Related: 

___

# Referencia de cliente en listado sale.order

> Añadimos la referencia del cliente en `sale.order` dentro de:
> 	- Presupuestos
> 	- Pedidos de venta

```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
	
	<!-- PRESUPUESTO -->
    <record id="pnt_sale_list" model="ir.ui.view">  
        <field name="name">pnt.sale.list</field>  
        <field name="model">sale.order</field>  
        <field name="inherit_id" ref="sale.view_quotation_tree_with_onboarding"/>  
        <field name="arch" type="xml">  
            <xpath expr="//field[@name='create_date']" position="after">  
                <field name="client_order_ref" readonly="1"/>  
            </xpath>  
        </field>  
    </record>  
    
	<!-- PEDIDO DE VENTA -->
    <record id="pnt_sale_order_list" model="ir.ui.view">  
        <field name="name">pnt.sale.order.list</field>  
        <field name="model">sale.order</field>  
        <field name="inherit_id" ref="sale.view_order_tree"/>  
        <field name="arch" type="xml">  
            <xpath expr="//field[@name='date_order']" position="after">  
                <field name="client_order_ref" readonly="1"/>  
            </xpath>  
        </field>  
    </record>  
    
</odoo>
```

![[Pasted image 20240202094257.png]]

[[Añadir filtro de referencia de cliente]]