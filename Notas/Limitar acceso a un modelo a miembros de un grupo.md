> [[Back]]

Tags: 
Status: 
Related: 

___

# Limitar acceso a un modelo a miembros de un grupo

> Creamos un grupo nuevo para permitir acceso a un modelo determinado.

### Creamos `security/res_groups.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <record id="pnt_invoicing_accounting_group" model="res.groups">  
        <field name="name">Invoicing / Accounting</field>  
        <field name="implied_ids" eval="[(4, ref('base.group_user'))]"/>  
        <field name="users" eval="[(4, ref('base.user_root'))]"/>  
    </record>  
</odoo>
```

### Especificamos el grupo en `security/ir.model.access.csv`
```python
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink  
access_pnt_redirect_app,Access pnt.redirect.app,model_pnt_redirect_app,custom_pnt.pnt_invoicing_accounting_group,1,1,1,1
```