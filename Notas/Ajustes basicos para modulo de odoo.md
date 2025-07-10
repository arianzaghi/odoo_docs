> [[Añadir ajustes para módulo odoo]]

Tags: 
Status: 
Related: 

___

# Ajustes basicos para modulo de odoo
## Modelo Ajustes
### Python
```python
from odoo import fields, models


class ResConfigSettings(models.TransientModel):
    _inherit = 'res.config.settings'

    pnt_max_provider_limit = fields.Float(
        string="Maximum limit to spend on a provider and on a project",
        default=lambda self: float(
            self.env['ir.config_parameter'].sudo().get_param('project.pnt_max_provider_limit', default=0.0))
    )

    def set_values(self):
        super(ResConfigSettings, self).set_values()
        self.env['ir.config_parameter'].sudo().set_param('project.pnt_max_provider_limit', self.pnt_max_provider_limit)
```
### Vista Ajustes
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<odoo>
    <record id="pnt_" model="ir.ui.view">
        <field name="model">res.config.settings</field>
        <field name='inherit_id' ref='custom_pnt.pnt_res_config_settings_view_form_project'/>
        <field name="priority" eval="999"/>
        <field name="arch" type="xml">
            <xpath expr="//setting[@id='proyect_max_hours_per_day']" position="after">
                <setting id="pnt_max_limit" help="Maximum limit to spend on a provider.">
                    <field name="pnt_max_provider_limit"/>
                </setting>
            </xpath>
        </field>
    </record>
</odoo>
```

## Llamada al ajuste 
```python
class PurchaseOrder(models.Model):
    _inherit = 'purchase.order'

    def button_confirm(self):
        limit = float(
            self.env['ir.config_parameter'].sudo().get_param('project.pnt_max_provider_limit', default=14999.99))
```
#### [Redit_HU58648 - Max provider limit](https://github.com/puntsistemes/redit_odoo/pull/5/files#diff-f3152ddeb0bd7b3ea8920307c9c57dc342d6effa5b68b767ee7d964c03a30b3b)
#### [[Palacio_HU53580 - Modelo ponderacion horas extra con ajustes]]