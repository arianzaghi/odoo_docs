> [[]]

Tags: 
Status: 
Related: [[Redirect App]]

___

# Añadir ajustes para módulo odoo



![[Pasted image 20240715110215.png]]

## Programación
![[Pasted image 20240715110104.png]]
### Vistas
#### `res_config_settings_views.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <data>  
        <record id="res_config_settings_view_form" model="ir.ui.view">  
            <field name="name">res.config.settings.view.redirect.app</field>  
            <field name="model">res.config.settings</field>  
            <field name="priority" eval="40"/>  
            <field name="inherit_id" ref="base.res_config_settings_view_form"/>  
            <field name="arch" type="xml">  
                <xpath expr="//div[hasclass('settings')]" position="inside">  
                    <div class="app_settings_block" data-string="Redirect App" id="redirect_app" string="Redirect App"  
                         data-key="redirect_app" groups="base.group_system">  
                        <h2>Redirect App Settings</h2>  
                        <div class="row mt16 o_settings_container" id="redirect_app_settings">  
                            <div class="col-12 col-lg-6 o_settings_box">  
                                <div class="o_settings_right_pane">  
                                    <span class="o_form_label">URL URL URL</span>  
                                    <div class="text-muted content-group mt16">  
                                        <field name="pnt_report_url" class="text-center oe_inline">  
                                            <span>URL URL URL 2</span>  
                                        </field>  
                                    </div>  
                                </div>  
                            </div>  
                        </div>  
                    </div>  
                </xpath>  
            </field>  
        </record>  
  
        <record id="pnt_redirect_app_settings_action" model="ir.actions.act_window">  
            <field name="name">Redirect app settings</field>  
            <field name="type">ir.actions.act_window</field>  
            <field name="res_model">res.config.settings</field>  
            <field name="view_mode">form</field>  
            <field name="target">inline</field>  
            <field name="context">{'module' : 'redirect_app', 'bin_size': False}</field>  
        </record>  
  
        <menuitem id="pnt_redirect_app_settings"  
                  name="Redirect App Settings"  
                  parent="redirect_app.menu_redirect_app1"  
                  sequence="0"  
                  action="pnt_redirect_app_settings_action"  
                  groups="base.group_system"/>  
    </data>  
</odoo>
```
##### Desglose
**Vista principal**
```xml
<record id="res_config_settings_view_form" model="ir.ui.view">  
	<field name="name">res.config.settings.view.redirect.app</field>  
	<field name="model">res.config.settings</field>  
	<field name="priority" eval="40"/>  
	<field name="inherit_id" ref="base.res_config_settings_view_form"/>  
	<field name="arch" type="xml">  
		<xpath expr="//div[hasclass('settings')]" position="inside">  
			<div class="app_settings_block" data-string="Redirect App" id="redirect_app" string="Redirect App"  
				 data-key="redirect_app" groups="base.group_system">  
				<h2>Redirect App Settings</h2>  
				<div class="row mt16 o_settings_container" id="redirect_app_settings">  
					<div class="col-12 col-lg-6 o_settings_box">  
						<div class="o_settings_right_pane">  
							<span class="o_form_label">URL URL URL</span>  
							<div class="text-muted content-group mt16">  
								<field name="pnt_report_url" class="text-center oe_inline">  
									<span>URL URL URL 2</span>  
								</field>  
							</div>  
						</div>  
					</div>  
				</div>  
			</div>  
		</xpath>  
	</field>  
</record>  
```
**Menu item**
```xml
<menuitem id="pnt_redirect_app_settings"  
          name="Redirect App Settings"  
          parent="redirect_app.menu_redirect_app1"  
          sequence="0"  
          action="pnt_redirect_app_settings_action"  
          groups="base.group_system"/>
```
**Action**
```xml
<record id="pnt_redirect_app_settings_action" model="ir.actions.act_window">  
    <field name="name">Redirect app settings</field>  
    <field name="type">ir.actions.act_window</field>  
    <field name="res_model">res.config.settings</field>  
    <field name="view_mode">form</field>  
    <field name="target">inline</field>  
    <field name="context">{'module' : 'redirect_app', 'bin_size': False}</field>  
</record>
```

****

**Herencia de `res.config.settings`**
```python
from odoo import fields, models  
  
  
class ResConfigSettings(models.TransientModel):  
    _inherit = 'res.config.settings'  

	# Creamos los campos que necesitamos monstrar en ajustes
    pnt_report_url = fields.Char(string="Url")
```


### Python
#### `res_config_settings.py`
```python
from odoo import fields, models  
  
  
class ResConfigSettings(models.TransientModel):  
    _inherit = 'res.config.settings'  
  
    pnt_report_url = fields.Char(string="Url")
```
#### `__manifest__.py`
```python
{  
    'name': 'Redirect App',  
    'version': '16.0.0.0',  
    'summary': 'App that redirects to a website URL',  
    'description': 'An app icon that redirects to a website URL',  
    'author': 'Your Name',  
    'category': 'Tools',  
    'depends': [  
        'base_pnt',  
        'base',  
    ],  
    'data': [  
        'views/redirect_app_views.xml',  
        'views/res_config_settings_views.xml',  
    ],  
    'assets': {  
        'web.assets_backend': [  
            'redirect_app/static/description/sek_1.png',  
            'redirect_app/static/description/sek_2.png',  
            'redirect_app/static/description/sek_3.png',  
            'redirect_app/static/description/sek_4.png',  
        ],  
    },  
    'installable': True,  
    'application': True,  
}
```