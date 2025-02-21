> [[040 - Python framework]]

Tags: 
Status: 
Related: 

___

# Acción de vista tree para ejecutar masivamente acciones de form

> **Problema:** tenemos en la vista form un método (cancelar factura, pasar a borrador....) y queremos ejecutarlo para muchos registros sin tener que ir uno a uno
> **Solución:** Botón acción que permita llamar al método para todos los registros.


**Action**
```xml
<record id="action_renew_suscription" model="ir.actions.server">  
    <field name="name">Renew Suscriptions</field>  
    <field name="model_id" ref="sale.model_sale_order"/>  
    <field name="binding_model_id" ref="sale.model_sale_order"/>  
    <field name="binding_view_types">list</field>  
    <field name="state">code</field>  
    <field name="code">action = records.action_renew_suscription()</field>  
</record>
```

**Metodo iterativo**
```python
def action_renew_suscription(self):  
    suscriptions = self.filtered(  
        lambda x: x.id  
        and x.stage_category == "progress"  
        and x.state == "sale"  
    )  
  
    if not suscriptions:  
        raise UserError(_("There are no subscriptions to renew."))  
    for suscription in suscriptions:  
        suscription.prepare_renewal_order()
```

## Accion en `sale.order`
![[Pasted image 20241121165149.png]]

`sale_order_views.xml`
```xml
<record id="action_generate_pos" model="ir.actions.server">  
    <field name="name">Generate Purchase Orders</field>  
    <field name="model_id" ref="sale.model_sale_order"/>  
    <field name="binding_model_id" ref="sale.model_sale_order"/>  
    <field name="binding_view_types">list</field>  
    <field name="state">code</field>  
    <field name="code">action = records.action_generate_purchase_order()</field>  
</record>
```

`sale_order.py`
```python
class SaleOrder(models.Model):  
    _inherit = "sale.order"

def action_generate_purchase_order(self):  
    for order in self:  
    # ... code ....
```

## Accion en `account.move`

> https://github.com/puntsistemes/fluidthermal_odoo/pull/13/commits/db2a571d16142925a1d87071087658daed10a0a4

`account_move_views.xml`
```xml
<record id="pnt_action_reset_all_to_draft" model="ir.actions.server">  
    <field name="name">Restore to draft</field>  
    <field name="model_id" ref="account.model_account_move"/>  
    <field name="binding_model_id" ref="sale.model_account_move"/>  
    <field name="binding_view_types">list</field>  
    <field name="state">code</field>  
    <field name="code">action = records.pnt_massive_button_draft()</field>  
</record>
```

`account_move.py`
```python
from odoo import models, fields, api  
  
class PntAccountMove(models.Model):  
    _inherit = 'account.move'  
  
    def pnt_massive_button_draft(self):  
        for move in self:  
            move.button_draft()
```