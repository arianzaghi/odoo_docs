> [[Back]]

Tags: 
Status: 
Related: [[res.partner]]

___

# Mostrar usuarios archivados en campo comercial del contacto

> Queremos que los usuarios `res.user` que están archivados se muestren
> en el seleccionable de `Comercial` de nuestro contacto `res.partner`

### **`res.partner`**
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <record id="pnt_res_partner_form_view" model="ir.ui.view">  
        <field name="model">res.partner</field>  
        <field name="name">pnt.res.partner.view.form</field>  
        <field name="inherit_id" ref="base.view_partner_form"/>  
        <field name="arch" type="xml">  
            <xpath expr="//group[@name='sale']//field[@name='user_id']" position="attributes">  
                <attribute name="domain">[('share','=',False),('active','in',[1,0])]</attribute>  
                <attribute name="options">{'no_create': True}</attribute>  
            </xpath>  
        </field>  
    </record>  
</odoo>
```

- Faltan 2 partes para constituir modulo comisiones