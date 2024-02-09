> [[Odoo Modelos]]

Tags: 
Status: 
Related: 

___

# Modelo Mantenimiento

Modelo nuevo que permite a los usuarios crear nuevos registros para asignárselos a otros modelos.


#### Clase "Hobbies". Almacena el nombre, el partner y el color.
```python
from odoo import models, fields, api
from random import randint
from odoo.exceptions import ValidationError


class PntResPartnerHobbies(models.Model):
    _description = "Partner hobbies and skills"
    _name = "pnt.res.partner.hobbies"
    _order = "pnt_name"
    _rec_name = "pnt_name"

	# Generador de colores para las etiquetas
    def _get_default_color(self):
        return randint(1, 11)

    pnt_name = fields.Char(string="Hobby or skill", required=True, translate=True)
    partner_ids = fields.Many2many("res.partner", string="Partners")
    pnt_color = fields.Integer(string="Color", default=_get_default_color)
```

Vista **FORM** para crear y editar hobbies y skills.
```python
<record id="pnt_res_partner_hobbies_view_form" model="ir.ui.view">  
	<field name="name">pnt.res.partner.hobbies.view.form</field>  
	<field name="model">pnt.res.partner.hobbies</field>  
	<field name="arch" type="xml">  
		<form string="hobbies">  
			<group>  
				<field name="pnt_name" />  
			</group>  
		</form>  
	</field>  
</record>
```

Vista **LIST** para crear y editar hobbies y skills.
```python  
<record id="pnt_res_partner_hobbies_view_tree" model="ir.ui.view">  
	<field name="name">pnt.res.partner.hobbies.view.tree</field>  
	<field name="model">pnt.res.partner.hobbies</field>  
	<field name="arch" type="xml">  
		<tree editable="bottom" class="hobbies_tree">  
			<field name="pnt_name" />  
		</tree>  
	</field>  
</record>
```


```python
<record id="pnt_res_partner_hobbies_action" model="ir.actions.act_window">  
	<field name="name">Hobbies and skills</field>  
	<field name="res_model">pnt.res.partner.hobbies</field>  
	<field name="view_mode">tree,form</field>  
	<field name="help" type="html">  
		<p class="o_view_nocontent_smiling_face">No items created.</p>  
	</field>  
</record>  
```

```python
<record id="pnt_res_partner_hobbies_tree" model="ir.actions.act_window.view">  
	<field eval="1" name="sequence"/>  
	<field name="view_mode">tree</field>  
	<field name="view_id" ref="pnt_res_partner_hobbies_view_tree"/>  
	<field name="act_window_id" ref="pnt_res_partner_hobbies_action"/>  
</record>  
```
  
```python
<record id="pnt_res_partner_hobbies_act_view_form" model="ir.actions.act_window.view">  
	<field eval="2" name="sequence"/>  
	<field name="view_mode">form</field>  
	<field name="view_id" ref="pnt_res_partner_hobbies_view_form"/>  
	<field name="act_window_id" ref="pnt_res_partner_hobbies_action"/>  
</record>  
```
  
```python
<record id="pnt_res_partner_hobbies_menu" model="ir.ui.menu">  
	<field name="name">Hobbies and skills</field>  
	<field name="action" ref="pnt_res_partner_hobbies_action"/>  
	<field name="parent_id" ref="contacts.res_partner_menu_contacts"/>  
	<field name="sequence">22</field>  
</record>  
```

## Ejemplos

### 1. Bonagent - Hobbies y Skills
[Github](https://github.com/puntsistemes/bona-gent_odoo/pull/44/commits/8378d1e09d1d3c4e87bd098ae3f39e6e1860696e#diff-8b857d45237d44ffe08a8959e63446c96c803486e5256a39dd6be3b994280403)

### 2. Franja95 - Alérgenos


