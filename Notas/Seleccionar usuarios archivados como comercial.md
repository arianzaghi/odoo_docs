> [[domain]]

Tags: 
Status: 
Related: 

___

# Seleccionar usuarios archivados como comercial

> Se ha de poder seleccionar como Comercial en la ficha de los clientes a usuarios de Odoo en estado Archivado.

![[Pasted image 20240409090209.png]]

## Solución

`res_partner.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
	<record id="view_partner_form" model="ir.ui.view">
        <field name="model">res.partner</field>
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

- `('share','=',False)` excluye a los usuarios del portal

## Ejemplos

[mantra](https://github.com/puntsistemes/mantra-iluminacion_odoo/blob/14.0/custom_pnt/views/res_partner.xml#L81)
[dolz](https://github.com/puntsistemes/dolz_odoo/pull/2/commits/6e6454e14383101cb78486f8e47d9f49f2bf8cee#diff-9a53cca74818590b5964e787dd2eae79c2e7ac1e5cedcb385e5b7e564bbdb459)