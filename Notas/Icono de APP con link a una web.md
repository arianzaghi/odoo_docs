> [[Redirect App]]

Tags: 
Status: 
Related: 

___

# Icon de APP con link a una web

> Módulo (icono de app en menu principal) que al hacerle click nos redirige a una web externa

![[Pasted image 20240628090712.png]]

### `schema`
![[Pasted image 20240628090642.png]]

### `redirect_app_views.xml`
```xml
<odoo>  
    <data>  
        <!-- Create an action to open the URL -->  
        <record id="action_redirect_website" model="ir.actions.act_url">  
            <field name="name">Redirect to Website</field>  
            <field name="type">ir.actions.act_url</field>  
            <field name="url">https://vda10-2020.sek.net/erpsek-master/</field>  
            <field name="target">new</field>  
        </record>  
  
        <!-- Create a menu item to show the app icon -->  
        <menuitem id="menu_redirect_app"  
                  name="Redirect App"  
                  action="action_redirect_website"  
                  web_icon="redirect_app/static/redirect_icon.png"/>  
    </data>  
</odoo>
```

### `__manifest__.py`
```python
{  
    'name': 'Redirect App',  
    'version': '16.0.0.0',  
    'summary': 'App that redirects to a website URL',  
    'description': 'An app icon that redirects to a website URL',  
    'author': 'Your Name',  
    'category': 'Tools',  
    'depends': [  
        'base_pnt'  
    ],  
    'data': [  
        'views/redirect_app_views.xml',  
    ],  
    'installable': True,  
    'application': True,  
}
```