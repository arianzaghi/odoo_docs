> [[Wizards]]

Tags: 
Status: 
Related: 

___
# Pasar registros por contexto a un wizard
> Cuando seleccionamos varios registros en el tree y abrimos el wizard, queremos que se guarden estos registros en el campo del popup del wizard.

**Pasamos el contexto al record de invocación del wizard**
```xml
<field name="context">{'default_pnt_product_pricelist_ids': active_ids}</field>
```
- `active_ids` = ids seleccionados en el modelo desde el que llamamos al wizard
- `default_pnt_product_pricelist_ids` = añadimos `default` + `nombre_del_campo` donde queremos guardar los valores

**Record de invocación**
```xml
<!-- Record de invocacion del wizard -->  
<record id="pnt_ipc_updater_wizard_action" model="ir.actions.act_window">  
    <field name="name">Update IPC Wizard</field>  
    <field name="res_model">pnt.ipc.updater.wizard</field>  
    <field name="view_mode">form</field>
    # AQUI
    <field name="context">{'default_pnt_product_pricelist_ids': active_ids}</field>  
    # AQUI  
    <field name="view_id" ref="pnt_ipc_updater_form_view"/>  
    <field name="target">new</field>  
    <field name="binding_model_id" ref="product.product_pricelist_view_tree"/>  
    <field name="binding_view_types">form</field>  
</record>
```