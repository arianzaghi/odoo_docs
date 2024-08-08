> [[Modulos custom de punt]]

Tags: 
Status: 
Related: 

___

# Redirect App
> [Educonsul v16](https://github.com/puntsistemes/educonsul_odoo/commit/382e7f9d09a69432650681074bacca22ed5f0fe6)
> 
> ![[Pasted image 20240715133602.png]]

- [[Icono de APP con link a una web]]
- [[Añadir ajustes para módulo odoo]]
- [[Limitar acceso a un modelo a miembros de un grupo]]


## V1
> Nuestro modelo no contiene el dato, lo recoje del parametro que se configura desde ajustes.

### Python
#### `redirect_app.py`
```python
from odoo import models, fields, api  
  
default_url = "https://vda10-2020.sek.net/erpsek-master/"  
  
  
class PntRedirectApp(models.Model):  
    _inherit = "ir.actions.act_url"  
    _description = "App module that redirects to a custom link. (Settings > )"  
  
    @api.model  
    def create(self, vals):  
        if vals.get('url') == '%(pnt_redirect_url)d':  
            vals['url'] = self.env['ir.config_parameter'].sudo().get_param('pnt.redirect.url', default='default_url')  
        return super(PntRedirectApp, self).create(vals)  
  
    def write(self, vals):  
        if vals.get('url') == '%(pnt_redirect_url)d':  
            vals['url'] = self.env['ir.config_parameter'].sudo().get_param('pnt.redirect.url', default='default_url')  
        return super(PntRedirectApp, self).write(vals)
```
#### `res_config_settings.py`
```python
from odoo import fields, models, api  
  
  
class ResConfigSettings(models.TransientModel):  
    _inherit = 'res.config.settings'  
  
    pnt_redirect_url = fields.Char(string="Url", config_parameter='pnt.redirect.url')
```

### Vistas
#### `redirect_app_views.xml`
```xml
<odoo>  
    <data>  
        <record id="action_redirect_website" model="ir.actions.act_url">  
            <field name="name">Redirect to Website</field>  
            <field name="type">ir.actions.act_url</field>  
            <field name="url">%(pnt_redirect_url)d</field>  
            <field name="target">new</field>  
        </record>  
  
        <menuitem id="menu_redirect_app1"  
                  name="Admon SEK"  
                  action="action_redirect_website"  
                  web_icon="redirect_app,static/description/sek_1.png"/>  
    </data>  
</odoo>
```
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
                                    <span class="o_form_label">Redirect URL</span>  
                                    <div class="text-muted content-group mt16">  
                                        <field name="pnt_redirect_url" class="text-start oe_inline">  
                                            <span>Redirect URL</span>  
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

## V2

> Nuestro modelo contiene el dato, y se actualiza cuando lo cambiamos desde ajustes. El icono lee el dato del modelo.

### Python
#### `redirect_app.py`
```python
from odoo import models, fields, api  
  
  
class PntRedirectApp(models.Model):  
    _name = "pnt.redirect.app"  
    _description = "App module that redirects to a custom link."  
    _rec_name = "pnt_redirect_url"  
  
    pnt_redirect_url = fields.Char(string="URL")  
  
    @api.model  
    def get_redirect_action(self):  
        redirect_url = self.search([], limit=1).pnt_redirect_url  
        if not redirect_url:  
            redirect_url = 'https://vda10-2020.sek.net/erpsek-master/'  
        action = {  
            'type': 'ir.actions.act_url',  
            'url': redirect_url,  
            'target': 'new',  
        }  
        return action
```
#### `res_config_settings.py`
```python
from odoo import models, fields, api  
  
  
class ResConfigSettings(models.TransientModel):  
    _inherit = 'res.config.settings'  
  
    pnt_redirect_url = fields.Char(string="Redirect URL", config_parameter='pnt.redirect.url')  
  
    @api.model  
    def set_values(self):  
        super(ResConfigSettings, self).set_values()  
        redirect_url = self.env['ir.config_parameter'].sudo().get_param('pnt.redirect.url')  
        redirect_app = self.env['pnt.redirect.app'].search([], limit=1)  
        if not redirect_app:  
            self.env['pnt.redirect.app'].create({'pnt_redirect_url': redirect_url})  
        else:  
            redirect_app.write({'pnt_redirect_url': redirect_url})
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
        'custom_pnt',  
        'base',  
    ],  
    'data': [  
        'security/ir.model.access.csv',  
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

### Vistas
#### `redirect_app_views.xml`
```xml
<odoo>  
    <data>  
        <record id="action_redirect_website" model="ir.actions.server">  
            <field name="name">Redirect to Website</field>  
            <field name="model_id" ref="model_pnt_redirect_app"/>  
            <field name="binding_model_id" ref="model_pnt_redirect_app"/>  
            <field name="state">code</field>  
            <field name="code">action = model.get_redirect_action()</field>  
        </record>  
  
        <menuitem id="menu_redirect_app"  
                  name="Admon SEK"  
                  action="action_redirect_website"  
                  web_icon="redirect_app,static/description/sek_1.png"  
        />  
    </data>  
</odoo>
```
#### `res_config_settings_views.xml` (same)
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
                                    <span class="o_form_label">Redirect URL</span>  
                                    <div class="text-muted content-group mt16">  
                                        <field name="pnt_redirect_url" class="text-start oe_inline">  
                                            <span>Redirect URL</span>  
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
                  parent="redirect_app.menu_redirect_app"  
                  sequence="0"  
                  action="pnt_redirect_app_settings_action"  
                  groups="base.group_system"/>  
    </data>  
</odoo>
