> [[Modelo Mantenimiento]]

Tags: 
Status: 
Related: 

___

# Modelo mantenimiento con TREE

[Bonagent v15](https://github.com/puntsistemes/bona-gent_odoo/commit/4efffc0753a26ba9d4d4c3ae92362a7c6480be00)

## Modelo del mantenimiento
```python
from odoo import models, fields  
  
  
class PntResPartnerJob(models.Model):  
    _name = "pnt.res.partner.job"  
    _description = "Jobs"  
    _rec_name = "pnt_name"  
  
    pnt_name = fields.Char(string="name")  
    pnt_description = fields.Text(string="Description", required=False)
```

## Modelo relacional, `matenimiento_tree` y clase destino
```python
from odoo import models, fields  
  
class PntResPartnerJobRelation(models.Model):  
    _name = "pnt.res.partner.job.relation"  
    _description = "Res Partner Job Relation"  
    _rec_name = "pnt_observation"  
  
    pnt_observation = fields.Text(string="Observation")  
    pnt_partner_id = fields.Many2one(string="Jobs", comodel_name="res.partner")  
    pnt_job_id = fields.Many2one(string="Jobs", comodel_name="pnt.res.partner.job")
```


## Vistas del modelo `mantenimiento_tree.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data>

        <record id="pnt_res_partner_company_car_view_tree" model="ir.ui.view">
            <field name="name">pnt.res.partner.company.car.view.tree</field>
            <field name="model">pnt.res.partner.company.car</field>
            <field name="arch" type="xml">
                <tree editable="bottom">
                    <field name="pnt_name"/>
                </tree>
            </field>
        </record>

        <record id="pnt_res_partner_company_car_view_form" model="ir.ui.view">
            <field name="name">pnt.res.partner.company.car.view.form</field>
            <field name="model">pnt.res.partner.company.car</field>
            <field name="arch" type="xml">
                <form string="Vehicle permissions">
                    <group>
                        <field name="pnt_name"/>
                    </group>
                </form>
            </field>
        </record>

        <record id="pnt_res_partner_company_car_action" model="ir.actions.act_window">
            <field name="name">Vehicle Permissions</field>
            <field name="res_model">pnt.res.partner.company.car</field>
            <field name="view_mode">tree,form</field>
            <field name="help" type="html">
                <p class="o_view_nocontent_smiling_face">No items created.</p>
            </field>
        </record>

        <record id="pnt_res_partner_company_car_tree"
                model="ir.actions.act_window.view">
            <field eval="1" name="sequence"/>
            <field name="view_mode">tree</field>
            <field name="view_id" ref="pnt_res_partner_company_car_view_tree"/>
            <field name="act_window_id" ref="pnt_res_partner_company_car_action"/>
        </record>

        <record id="pnt_res_partner_company_car_act_view_form"
                model="ir.actions.act_window.view">
            <field eval="2" name="sequence"/>
            <field name="view_mode">form</field>
            <field name="view_id" ref="pnt_res_partner_company_car_view_form"/>
            <field name="act_window_id" ref="pnt_res_partner_company_car_action"/>
        </record>


        <record id="pnt_res_partner_company_car_menu" model="ir.ui.menu">
            <field name="name">Vehicle permissions</field>
            <field name="action" ref="pnt_res_partner_company_car_action"/>
            <field name="parent_id" ref="contacts.res_partner_menu_contacts"/>
            <field name="sequence">13</field>
        </record>
    </data>
</odoo>
```

## Vista de la relación `res.partner`
```xml
<field name="pnt_partner_job_experience_ids" string="Job Experiences">
	<tree>
		<field name="pnt_job_id"/>
		<field name="pnt_observation"/>
	</tree>
</field>
```

## Security
```python
{{MÓDULO}}.access_{{MODELO}},access_{{MODELO}},{{MÓDULO}}.model_{{MODELO}},base.group_user,1,1,1,1
```
### **Ejemplo**
```python
custom_pnt.access_pnt_res_partner_hobbies,access_pnt_res_partner_hobbies,custom_pnt.model_pnt_res_partner_hobbies,base.group_user,1,1,1,1
```
