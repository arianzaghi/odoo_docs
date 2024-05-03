%%  %%> [[Wizards]]

Tags: 
Status: 
Related: 

___

# Wizard Impresion Etiqueta

![[Pasted image 20240428211442.png]]
## Programación paso a paso
### Vistas
#### Wizard
> **Vista XML del wizard popup donde introducimos los datos y el record que lo invoca**
```xml
<!-- Vista del WIZARD -->
<record id="out_picking_label_wizard_form_view" model="ir.ui.view">  
    <field name="name">out.picking.label.wizard.form.view</field>  
    <field name="model">out.picking.label.wizard</field>  
    <field name="arch" type="xml">  
        <form>  
            <sheet>  
                <group>  
                    <field name="qty"/>  
                    <field name="weight"/>  
                    <field name="pallet"/>  
                    <field name="agency"/>  
                    <field name="delivery"/>  
                    <field name="transport"/>  
                </group>  
                <footer>  
                    <button name="print_labels" type="object" string="Print"  
                            class="oe_highlight"/>  
                    <button special="cancel" string="Cancel" type="object"  
                            class="btn btn-default oe_inline"/>  
                </footer>  
            </sheet>  
        </form>  
    </field>  
</record>

<!-- Record de invocacion del wizard -->
<record id="pnt_out_picking_label_wizard_action" model="ir.actions.act_window">  
    <field name="name">Imprimir etiquetas 50x50</field>  
    <field name="res_model">out.picking.label.wizard</field>  
    <field name="view_mode">form</field>  
    <field name="context">{'default_picking_id': active_id}</field>  
    <field name="view_id" ref="out_picking_label_wizard_form_view"/>  
    <field name="target">new</field>  
    <field name="binding_model_id" ref="stock.model_stock_picking"/>  
    <field name="binding_view_types">form</field>  
</record>
```
### Etiqueta
> **XLM del informe (etiqueta) y su record de invocacion**
```xml
<!-- ETIQUETA -->
<template id="report_pnt_out_picking_label_document">  
    <t t-call="web.basic_layout">  
        <div class="page">  
            <div style="text-align:center;
                page-break-after:always;
                margin-top:45px;
                margin:0 -15px!important">
                
                <p style="font-size:1rem;line-height:.8rem;">  
                    <strong>Nº LotA.</strong>  
                    <strong t-field="docs.qty"/>  
                    <strong t-field="docs.weight"/>  
                    <strong t-field="docs.picking_id"/>  
                </p>  
            </div>  
        </div>  
    </t>  
</template>

<!-- Record de invocacion de etiqueta -->
<record id="report_out_picking_label_wizard_action" model="ir.actions.report">  
    <field name="name">Print label</field>  
    <field name="model">out.picking.label.wizard</field>  
    <field name="report_type">qweb-pdf</field>  
    <field name="report_name">report_pnt.report_pnt_out_picking_label_document</field>  
    <field name="report_file">report_pnt.report_pnt_out_picking_label_document</field>  
    <field name="print_report_name">'Label'</field>  
    <field name="binding_type">report</field>  
    <field name="paperformat_id" ref="report_pnt.paperformat_pnt_label"/>  
</record>
```

### Botón Activación Wizard
> **Añadimos los botones en `stock.picking`**
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <record id="pnt_stock_picking_form" model="ir.ui.view">  
        <field name="model">stock.picking</field>  
        <field name="inherit_id" ref="stock.view_picking_form"/>  
        <field name="arch" type="xml">  
            <xpath expr="//header" position="inside">  
                <button name="%(pnt_in_picking_label_wizard_action)d" string="Label Wizard" type="action" class="btn btn-success"/>  
                <button name="%(pnt_out_picking_label_wizard_action)d" string="Label Wizard" type="action" class="btn btn-success"/>  
                <button name="%(print_out_picking_action)d" string="Print Label" type="action" class="btn btn-success"/>  
            </xpath>  
        </field>  
    </record>  
</odoo>
```

### Modelos
#### Clase del Wizard
> **Clase tipo `TransientModel` sobre la que creamos el wizard**

> [!IMPORTANT] Registro de etiquetas
> Si no necesitamos guardar un registro de etiquetas, crearemos nuestro modelo como `TransientModel` de forma que no se guardarán datos de las clases.

```python
from odoo import api, fields, models, _  
from odoo.exceptions import UserError, ValidationError  
import logging  
  
  
class OutPickingLabelWizard(models.TransientModel):  
    _name = "out.picking.label.wizard"  
    _description = "Out Picking Label Wizard"  
  
    picking_id = fields.Many2one(comodel_name="stock.picking", string="Stock Picking")  

	# Opcional en caso de que queramos usar `Model`
	# y guardar los datos de las etiquetas en la
	# clase etiqueta
    out_label_id = fields.Many2one(  
        "pnt.out.picking.label",  
        string="Stock Move Line",  
        readonly=False,  
    )  
  
    qty = fields.Integer(string="Quantity of packages")  
    weight = fields.Integer(string="Quantity of Kilos")  
    pallet = fields.Char(string="Pallet")  
    agency = fields.Char(string="Agency")  
    delivery = fields.Char(string="Delivery")  
    transport = fields.Char(string="Transport")  
  
    def print_labels(self):  
        report = self.env["ir.actions.report"]._get_report(  
            "report_pnt.report_out_picking_label_wizard_action"  
        )  
        return report.report_action(self)
```

### Security

**Copy-Paste**
```python
{{MODULO}}.access_{{MODELO}},access_{{MODELO}},{{MODULO}}.model_{{MODELO}},base.group_user,1,1,1,1
```
- Reemplazamos `{{MODULO}}` por `module_name` (`custom_pnt`)
- Reemplazamos `{{MODELO}}` por `model_name` (`pnt_test_class`)

**Ejemplo**
```python
report_pnt.access_out_picking_label_wizard,access_out_picking_label_wizard,report_pnt.model_out_picking_label_wizard,base.group_user,1,1,1,1
```


#### Clase de la Etiqueta
> **Clase opcional, en caso de que queramos guardar registro de las etiquetas**

```python
class PntOutPickingLabel(models.TransientModel):  
    _name = "pnt.out.picking.label"  
    _description = "Pnt Out Picking Label"  
  
    picking_id = fields.Many2one(comodel_name="stock.picking", string="Stock Picking")  
    qty = fields.Integer(string="Quantity of packages")  
    weight = fields.Integer(string="Quantity of Kilos")  
    pallet = fields.Char(string="Pallet")  
    agency = fields.Char(string="Agency")  
    delivery = fields.Char(string="Delivery")  
    transport = fields.Char(string="Transport")
```
## Organización de carpetas

![[Pasted image 20240428230428.png]]

1. Creamos nuestro nuevo `modelo` llamado `wizards` donde guardamos todo lo relativo a los wizard
2. Creamos los modelos y vistas del wizard
	- `clase_wizard`
	- `vista_wizard`
		- `wizard_form_view_record`
		- `wizard_action_record`
3. Añadimos los ficheros py en el init
4. Declaramos las vistas y modelos
	- **init:** vistas de los wizard
	- **manifest:** `modelo` nuevo
5. Creamos la clase opcional y la declaramos en el init
6. Creamos los security para las clases creadas
7. IMPORTANTE: Añadimos la vista de `stock.picking` que contiene los botones del wizard en `views`
