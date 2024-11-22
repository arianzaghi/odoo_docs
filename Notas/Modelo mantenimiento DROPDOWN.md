> [[Modelo Mantenimiento]]

Tags: 
Status: 
Related: 

___

# Modelo mantenimiento dropdown

## Programación
### Modelo del mantenimiento
```python
from odoo import models, fields  
  
  
class Pnt{{NombreModelo}}(models.Model):  
    _name = "{{MODELO.}}"  
    _description = "{{DESCRIPTION}}"  
    _rec_name = "pnt_name"  
  
    pnt_name = fields.Char(string="name")  
    pnt_description = fields.Text(string="Description", required=False)
```

### Modelo de la clase destino
> Modelo en el que vamos a relacionar nuestra clase nueva para que el usuario pueda elegir un registro (`dropdown`)
```python
from odoo import models, fields  
  
class SaleOrderLine(models.Model):  
    _inherit = "sale.order.line"  
    
    pnt_sale_tag = fields.Many2one(
        "{{MODELO.}}",
        string="Sale Tag",
    )
```

### Vistas del modelo
> Vistas tree y form por defecto para nuestros modelos.

> [!Help] Ayuda
> Sustituimos por los campos del modelo
> ```
> {{MODELO_}} = nombre_del_modelo
> {{MODELO.}} = nombre.del.modelo
> {{FIELD}} = campo_del_modelo
> {{TITLE}} = titulo_del_modelo
> {{MENUITEM_VIEW_REF}} = id_del_menuitem_padre
> {{SEQUENCE}} = sequence_id
> ```

`mantenimiento_views.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data>
        <record id="{{MODELO_}}_view_tree" model="ir.ui.view">
            <field name="name">{{MODELO.}}.view.tree</field>
            <field name="model">{{MODELO.}}</field>
            <field name="arch" type="xml">
                <tree editable="bottom">
                    <field name="{{FIELD}}"/>
                </tree>
            </field>
        </record>
        
        <record id="{{MODELO_}}_view_form" model="ir.ui.view">
            <field name="name">{{MODELO.}}.view.form</field>
            <field name="model">{{MODELO.}}</field>
            <field name="arch" type="xml">
                <form string="{{TITLE}}">
                    <group>
                        <field name="{{FIELD}}"/>
                    </group>
                </form>
            </field>
        </record>
        
        <record id="{{MODELO_}}_action" model="ir.actions.act_window">
            <field name="name">{{TITLE}}</field>
            <field name="res_model">{{MODELO.}}</field>
            <field name="view_mode">tree,form</field>
            <field name="help" type="html">
                <p class="o_view_nocontent_smiling_face">No items created.</p>
            </field>
        </record>
        
        <record id="{{MODELO_}}_tree"
                model="ir.actions.act_window.view">
            <field eval="1" name="sequence"/>
            <field name="view_mode">tree</field>
            <field name="view_id" ref="{{MODELO_}}_view_tree"/>
            <field name="act_window_id" ref="{{MODELO_}}_action"/>
        </record>
        
        <record id="{{MODELO_}}_act_view_form"
                model="ir.actions.act_window.view">
            <field eval="2" name="sequence"/>
            <field name="view_mode">form</field>
            <field name="view_id" ref="{{MODELO_}}_view_form"/>
            <field name="act_window_id" ref="{{MODELO_}}_action"/>
        </record>
        
        <record id="{{MODELO_}}_menu" model="ir.ui.menu">
            <field name="name">{{TITLE}}</field>
            <field name="action" ref="{{MODELO_}}_action"/>
            <field name="parent_id" ref="{{MENUITEM_VIEW_REF}}"/>
            <field name="sequence">{{SEQUENCE}}</field>
        </record>
    </data>
</odoo>
```

### Vista de la relación `res.partner`
```xml
<field name="pnt_partner_job_experience_ids" string="Job Experiences">
	<tree>
		<field name="pnt_job_id"/>
		<field name="pnt_observation"/>
	</tree>
</field>
```

### Security
```python
{{MÓDULO}}.access_{{MODELO}},access_{{MODELO}},{{MÓDULO}}.model_{{MODELO}},base.group_user,1,1,1,1
```

## Ejemplos

### [Rankia v17 - Tipo de etiquetas en sale.order.line](https://github.com/puntsistemes/rankia_odoo/pull/4/files)