> [[Ajustes de odoo]]

Tags: 
Status: 
Related: 

___

# [Palacio_HU53580 - Modelo ponderacion horas extra con ajustes](https://github.com/puntsistemes/palacio-congresos_odoo/commit/95da37977f8906cc3814aae0c0658518fea136dc#diff-477988601c5159d47061eb894468c04c1df877a81ac2bf632bf773f0223af72a)

> Modelo para configurar el valor de las ponderaciones de horas extra cada año.
> Desde ajustes podemos ver la ponderación activa y crear nuevas.

![[Pasted image 20241126114706.png]]

```python
from odoo import fields, models, api
from datetime import date

class ResConfigSettings(models.TransientModel):
    _inherit = 'res.config.settings'
    selected_coefficient_id = fields.Many2one(
        'pnt.extra.hour.coefficient',
        string="Select Extra Hour Coefficient",
        default=lambda self: self._get_default_coefficient_id()
    )
    pnt_period_init_date = fields.Date(
        related='selected_coefficient_id.pnt_period_init_date',
        readonly=True
    )
    pnt_period_end_date = fields.Date(
        related='selected_coefficient_id.pnt_period_end_date',
        readonly=True
    )
    pnt_extra_ponderation = fields.Float(
        related='selected_coefficient_id.pnt_extra_ponderation',
        readonly=True
    )
    pnt_festive_ponderation = fields.Float(
        related='selected_coefficient_id.pnt_festive_ponderation',
        readonly=True
    )
    pnt_night_ponderation = fields.Float(
        related='selected_coefficient_id.pnt_night_ponderation',
        readonly=True
    )
    @api.model
    def _get_default_coefficient_id(self):
        today = date.today()
        active_period = self.env['pnt.extra.hour.coefficient'].search([
            ('pnt_period_init_date', '<=', today),
            ('pnt_period_end_date', '>=', today)
        ], limit=1)
        return active_period or False
```

`res_config_settings_views.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data>
        <record id="pnt_res_config_settings_view_form" model="ir.ui.view">
            <field name="name">res.config.settings.view.redirect.app</field>
            <field name="model">res.config.settings</field>
            <field name="priority" eval="40"/>
            <field name="inherit_id" ref="hr_attendance.res_config_settings_view_form"/>
            <field name="arch" type="xml">
                <xpath expr="//form//app[@name='hr_attendance']" position="inside">
                    <block title="Extra Hours Coefficients" name="extra_hours_coefficient">
                        <setting string="Active Ponderation Period" company_dependent="1">
                            <field name="selected_coefficient_id" class="w-75"/>
                            <group>
                                <field name="pnt_extra_ponderation" readonly="1"/>
                                <field name="pnt_festive_ponderation" readonly="1"/>
                                <field name="pnt_night_ponderation" readonly="1"/>
                            </group>
                            <group>
                                <field name="pnt_period_init_date" readonly="1"/>
                                <field name="pnt_period_end_date" readonly="1"/>
                            </group>
                        </setting>
                    </block>
                </xpath>
            </field>
        </record>
    </data>
</odoo>
```