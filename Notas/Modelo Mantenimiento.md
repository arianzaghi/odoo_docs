> [[Odoo Modelos]]

Tags: 
Status: 
Related: 

___

# Modelo Mantenimiento
Modelo nuevo que permite a los usuarios crear nuevos registros para asignárselos a otros modelos.

![[Pasted image 20240212135445.png]]
![[Pasted image 20240212135523.png]]

## Programación del modelo
### Clase Mantenimiento ("Hobbies").

Almacena el nombre, el partner y el color.
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

### Campo en la clase destino

##### Many2Many
```python
pnt_skills_hobbies = fields.Many2many(
	comodel_name="pnt.res.partner.hobbies",
	string="Hobbies and skills"
)
```

### Security
```python
{{MÓDULO}}.access_{{MODELO}},access_{{MODELO}},{{MÓDULO}}.model_{{MODELO}},base.group_user,1,1,1,1
```

**Ejemplo**
```python
custom_pnt.access_pnt_res_partner_hobbies,access_pnt_res_partner_hobbies,custom_pnt.model_pnt_res_partner_hobbies,base.group_user,1,1,1,1
```

### Vistas
#### List y Form para crear y editar hobbies y skills.
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

#### Cambiar el tipo de vista del mantenimiento
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

#### Representación de las etiquetas con colores en el modelo destino (`res.partner`)
```python
<field 
	name="pnt_allergy" widget="many2many_tags"
	options="{'color_field': 'pnt_color', 'no_create_edit': True}"
/>
```


### Acciones
#### Para nuestro Menu-item

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

#### Menu-item
Botón para navegar hasta nuestro mantenimiento

```python
<record id="pnt_res_partner_hobbies_menu" model="ir.ui.menu">  
	<field name="name">Hobbies and skills</field>  
	<field name="action" ref="pnt_res_partner_hobbies_action"/>  
	<field name="parent_id" ref="contacts.res_partner_menu_contacts"/>  
	<field name="sequence">22</field>  
</record>  
```

![[Pasted image 20240212132928.png]]




## Ejemplos

### 1. Mantenimiento: Hobbies y Skills - Bonagent
[Bonagent_47078](https://github.com/puntsistemes/bona-gent_odoo/pull/44/commits/8378d1e09d1d3c4e87bd098ae3f39e6e1860696e#diff-8b857d45237d44ffe08a8959e63446c96c803486e5256a39dd6be3b994280403)

### 2. Franja95 - Alérgenos
[Franja_47393](https://github.com/puntsistemes/franja15_odoo/pull/24/commits/7adbda9d47b2c3aa6b08943c49ae0e0da6b83a6a#diff-2697fb2e19b03477c3526f1be67c52df113a7f07da6f69c89207bbcaf9db7c4e)

### 3. Coralim - Métodos de transporte
[Coralim_48532](https://github.com/puntsistemes/coralim_odoo/pull/40/commits/92be2de68c909020681a81c3dbf989fab7c0e40f#diff-22c9f5d4c8f4aec79903a1ab223c4a663e1a523a15025aa792c984d02aa30febR1-R19)

### 4. Coralim - Dangerous goods packing group
[Coralim_48532](https://github.com/puntsistemes/coralim_odoo/pull/40/commits/92be2de68c909020681a81c3dbf989fab7c0e40f#diff-22c9f5d4c8f4aec79903a1ab223c4a663e1a523a15025aa792c984d02aa30febR1-R19)
