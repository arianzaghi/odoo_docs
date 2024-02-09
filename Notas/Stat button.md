> [[Odoo Views Vistas|Back]]

Tags: #xml #todo 
Status: 
Related: 

___

# Stat button

![[Pasted image 20240126075424.png]]
> [Docs reference](https://www.odoo.com/documentation/15.0/es/developer/tutorials/getting_started/12_sprinkles.html?highlight=buttons#stat-buttons)

# Añadir Stat button

> Queremos añadir un nuevo "Stat button" en `hr.employee` para navegar hasta las approvals pendientes del empleado, situadas en `multi.approval`
> 
> [som_energia](https://github.com/puntsistemes/som-energia_odoo/commit/9fac9198068b2fb2fda840f51e5a9416c6acd1ec)
> [HU45631](https://odoo.puntsistemes.com/web#id=45631&model=project.task&view_type=form&cids=1&menu_id=979)



- Devolvemos una vista a través de un botón de acción
  
```python
from odoo import fields, models, api, _


class PntHrEmployee(models.Model):
    _inherit = 'hr.employee'

	# Función que devuelve una vista de otro modelo
	def action_view_employee_requests(self):
		self.ensure_one()
		return {
			'name': _('Employee approvals'),
			'type': 'ir.actions.act_window',
			'res_model': 'multi.approval',
			'view_mode': 'tree,form',
			'context': {'search_default_filter_type':1},
			'domain': [('contact_id', 'in', self.related_contact_ids.ids)],
		}
```

- Colocamos nuestro Stat Button en `ref="hr.view_employee_form"`

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <record id="pnt_hr_employee_form" model="ir.ui.view">
        <field name="name">pnt.hr.employee.form</field>
        <field name="model">hr.employee</field>
        <field name="inherit_id" ref="hr.view_employee_form"/>
        <field name="arch" type="xml">
            <xpath expr="//div[@name='button_box']" position="inside">
                <button 
	                name="action_view_employee_requests"
	                string="Open Approvals"
	                type="object"
	                class="oe_highlight"
	                icon="fa-check-square" />
            </xpath>
        </field>
    </record>
</odoo>
```

- FIltros para despúes de la navegación a `hr.employee`

```xml
                <field name="pic_id" />
                <field name="type_id" />
                <group expand="1" string="Group By">
                    <filter string="User" name='user' context="{'group_by':'user_id'}"/>
                    <filter string="Type" name="type_id" context="{'group_by':'type_id'}"/>
                    <filter string="Status" name="status" context="{'group_by':'state'}"/>
                    <filter string="User" name='filter_user' context="{'group_by':'user_id'}"/>
                    <filter string="Type" name="filter_type" context="{'group_by':'type_id'}"/>
                    <filter string="Status" name="filter_status" context="{'group_by':'state'}"/>
                    <separator orientation="vertical" />
                    <filter string="Request Date" name="date" context="{'group_by':'request_date:month'}"/>
                    <filter string="Request Date" name="filter_date" context="{'group_by':'request_date:month'}"/>
                </group>
            </search>
        </field>
```