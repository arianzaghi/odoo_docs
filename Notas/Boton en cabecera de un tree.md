> [[033 - Boton]]

Tags: 
Status: 
Related: 

___
# Boton en cabecera de un tree

> Queremos añadir el botón `IPC Wizard` en la vista tree de un modelo.
![[Pasted image 20241126105342.png]]

> [!INFO] INFO
> En el caso de un `TREE`, lo ponemos dentro del header.
> En el caso de un `FORM`, lo pondríamos antes del header

## `product_pricelist_views.xml`
```xml
<record id="pnt_product_pricelist_view_tree" model="ir.ui.view">  
    <field name="name">product.pricelist.tree</field>  
    <field name="model">product.pricelist</field>  
    <field name="inherit_id" ref="product.product_pricelist_view_tree"/>  
    <field name="arch" type="xml">  
        <tree position="inside">  
            <header>  
                <button name="%(pnt_ipc_updater_wizard_action)d" string="IPC WIzard" type="action" class="btn btn-success"/>  
            </header>  
        </tree>  
    </field>  
</record>
```