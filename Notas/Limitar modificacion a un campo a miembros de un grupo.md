> [[Configuraciones de permisos]]

Tags: 
Status: 
Related: 

___
# Limitar modificacion a un campo a miembros de un grupo

> Tenemos un campo en un modelo que queremos que solo pueda ser modificado por miembros de un grupo

## 1. Creación del grupo

```xml
<record id="pnt_contact_tags_creation" model="res.groups">
	<field name="name">Contact Tags Creation</field>
</record>
```

## 2. Creación de la restricción

```python
class ResPartner(models.Model):
    _inherit = "res.partner"

    @api.onchange('category_id')
    def _onchange_category_id(self):
        if not self.env.user.has_group('nostrum_custom_cmnt.pnt_contact_tags_creation'):
            original_value = self._origin.category_id
            self.category_id = original_value
            return {
                'warning': {
                    'title': _('Access Denied'),
                    'message': _('You do not have the necessary permissions to modify this field.'),
                }
            }
```