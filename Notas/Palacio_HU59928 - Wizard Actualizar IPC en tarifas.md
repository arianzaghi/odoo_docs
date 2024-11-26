> [[Wizards]]

Tags: #HU
Status: 
Related: 
___
# [Palacio_HU59928 - Actualizar IPC en tarifas]()

> Wizard dentro de un tree para seleccionar registros y actualizarles el IPC. Pasamos los registros seleccionados por contexto.
![[Pasted image 20241126105342.png]]
![[Pasted image 20241126105410.png]]

## 1. [[Boton en cabecera de un tree]]
## 2. Wizard con seleccionable por medio
### Modelo
```python
class PntIPCUpdaterWizard(models.TransientModel):  
    _name = 'pnt.ipc.updater.wizard'  
    _description = 'IPC Updater Wizard'  
    _rec_name = 'pnt_ipc'  
  
    pnt_ipc = fields.Float('IPC', required=True)  
    pnt_product_pricelist_ids = fields.Many2many('product.pricelist', string='Pricelists to update')  
  
  
    def update_ipc(self):  
        for pricelist in self.pnt_product_pricelist_ids:  
            pricelist.update_pricelist_item_ipc(self.pnt_ipc)
```
### Vistas
#### Vista del wizard
```xml
<!-- Vista del WIZARD -->  
<record id="pnt_ipc_updater_form_view" model="ir.ui.view">  
    <field name="name">pnt.ipc.updater.form.view</field>  
    <field name="model">pnt.ipc.updater.wizard</field>  
    <field name="arch" type="xml">  
        <form>  
            <sheet>  
                <group>  
                    <field name="pnt_ipc"/>  
                    <field name="pnt_product_pricelist_ids" widget="many2many_tags"/>  
                </group>  
                <footer>  
                    <button name="update_ipc" type="object" string="Update IPC"  
                            class="oe_highlight"/>  
                    <button special="cancel" string="Cancel" type="object"  
                            class="btn btn-default oe_inline"/>  
                </footer>  
            </sheet>  
        </form>  
    </field>  
</record>
```
#### Record invocación wizard
```xml
<!-- Record de invocacion del wizard -->  
<record id="pnt_ipc_updater_wizard_action" model="ir.actions.act_window">  
    <field name="name">Update IPC Wizard</field>  
    <field name="res_model">pnt.ipc.updater.wizard</field>  
    <field name="view_mode">form</field>  
    <field name="context">{'default_pnt_product_pricelist_ids': active_ids}</field>  
    <field name="view_id" ref="pnt_ipc_updater_form_view"/>  
    <field name="target">new</field>  
    <field name="binding_model_id" ref="product.product_pricelist_view_tree"/>  
    <field name="binding_view_types">form</field>  
</record>
```
### 3. Pasar ids por contexto al wizard
> Cuando seleccionamos varios registros en el tree y abrimos el wizard, queremos que se guarden estos registros en el campo del popup del wizard.

**Pasamos el contexto al registro de invocación del wizard**
```xml
<field name="context">{'default_pnt_product_pricelist_ids': active_ids}</field>
```