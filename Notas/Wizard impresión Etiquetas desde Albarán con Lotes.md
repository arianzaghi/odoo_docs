> [[Wizards]]

Tags: 
Status: 
Related: 

___

# Wizard impresión Etiquetas desde Albarán con Lotes

![[Pasted image 20240503085502.png]]
![[Pasted image 20240503085632.png]]

## Programación
### Modelo Wizard `in_picking_label_wizard.py`
```python
from odoo import api, fields, models, _  
  
  
class InPickingLabelWizard(models.TransientModel):  
    _name = "in.picking.label.wizard"  
    _description = "In Picking Label Wizard"  
  
    picking_id = fields.Many2one(comodel_name="stock.picking", string="Stock Picking")  
    product_label_ids = fields.One2many(  
        "pnt.in.picking.label",  
        related="picking_id.product_label_ids",  
        string="Wizard Label ids",  
        readonly=False,  
    )  
  
  
    @api.model  
    def default_get(self, default_fields):  
        for elem in self.product_label_ids:  
            elem.unlink()  
        res = super(InPickingLabelWizard, self).default_get(default_fields)  
        picking_id = self.env["stock.picking"].browse(  
            self._context.get("default_picking_id")  
        )  
        if picking_id:  
            res["picking_id"] = picking_id.id  
            new_ids = []  
            for line in picking_id.move_line_ids:  
                quantity = line.quantity  
                label_id = self.env['pnt.in.picking.label'].create({  
                    'picking_id': line.picking_id.id,  
                    'product_id': line.product_id.id,  
                    'lot_id': line.lot_id.id,  
                    'product_packaging_id': line.product_packaging_id.id,  
                    'quantity_to_print': quantity,  
                    'qty_done': quantity,  
                })  
                new_ids.append(label_id.id)  
            if new_ids:  
                self.product_label_ids = [(6,0,new_ids)]  
                res['product_label_ids'] = [(6, 0, new_ids)]  
        return res  
  
    def print_labels(self):  
        picking_code = self.picking_id.picking_type_id.code  
        if picking_code == 'incoming':  
            report = self.env["ir.actions.report"]._get_report(  
                "report_pnt.pnt_in_picking_label_wizard_print_action"  
            )  
            return report.report_action(self)  
  
        elif picking_code == 'outgoing':  
            report = self.env["ir.actions.report"]._get_report(  
                "report_pnt.pnt_out_picking_abordo_label_wizard_print_action"  
            )  
            return report.report_action(self)
```

### Vista del wizard `in_picking_label_wizard.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <data>  
        <record id="in_picking_label_wizard_form_view" model="ir.ui.view">  
            <field name="name">in.picking.label.wizard.form.view</field>  
            <field name="model">in.picking.label.wizard</field>  
            <field name="arch" type="xml">  
                <form string="Etiquetas">  
                    <group>  
                        <group>  
                            <field name="picking_id" required="1" invisible="0"  
                                   readonly="1"/>  
                        </group>  
                    </group>  
                    <field name="product_label_ids"  
                           nolabel="1">  
                        <tree editable="bottom" create="0" delete="1">  
                            <field name="is_toggled"/>  
                            <field name="product_id" readonly="1"/>  
                            <field name="lot_id" readonly="1"/>  
                            <field name="quantity_to_print"/>  
                        </tree>  
                    </field>  
                    <footer>  
                        <button name="print_labels" type="object" string="Print"  
                                class="oe_highlight"/>  
                        <button special="cancel" string="Cancel" type="object"  
                                class="btn btn-default oe_inline"/>  
                    </footer>  
                </form>  
            </field>  
        </record>  
        
        <record id="pnt_in_picking_label_wizard_action" model="ir.actions.act_window">  
            <field name="name">Imprimir Etiquetas</field>  
            <field name="res_model">in.picking.label.wizard</field>  
            <field name="view_mode">form</field>  
            <field name="context">{'default_picking_id': active_id}</field>  
            <field name="view_id" ref="in_picking_label_wizard_form_view"/>  
            <field name="target">new</field>  
            <field name="binding_model_id" ref="stock.model_stock_picking"/>  
            <field name="binding_view_types">form</field>  
        </record>  
    </data>  
</odoo>
```


### Vista de etiqueta `pnt_in_picking_label`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="report_pnt_in_picking_label_document">  
        <t t-call="web.basic_layout">  
            <t t-set="product_label_ids" t-value="docs.product_label_ids"/>  
            <t t-foreach="docs.product_label_ids" t-as="label">  
                <t t-if="label.is_toggled">  
                    <t t-set="units" t-value="label.quantity_to_print"/>  
                    <t t-foreach="range(int(units) or 1)" t-as="unit">  
                        <div style="page-break-after:always; margin-top: 7%!important; border: solid white">  
                            <div class="row" style="margin-top: 6%">  
                                <div class="col-md-12">  
                                    <span style="margin-right: 2%">  
                                        <span>Entry Date</span>  
                                        <strong t-field="label.picking_id.date"  
                                                t-options='{"widget": "date","format": "dd/MM/yyyy"}'/>  
                                    </span>  
                                    <span style="margin-right: 2%">  
                                        <span>Nº:</span>  
                                        <strong t-field="label.picking_id"/>  
                                    </span>  
                                    <span style="margin-right: 2%">  
                                        <strong t-field="label.picking_id.partner_id.ref"/>  
                                    </span>  
                                </div>  
                            </div>  
                            <div class="col-md-12" style="margin-top: 5%">  
                                <span style="margin-right: 5%">  
                                    <strong t-field="label.product_id.default_code" style="text-decoration: underline;"/>  
                                </span>  
                            </div>  
                            <span>  
                                <strong t-field="label.product_id.name" style="text-decoration: underline;"/>  
                            </span>  
                            <div class="row" style="margin-top:4%">  
                                <table class="table mb64">  
                                    <tr>  
                                        <th class="text-start">Lot Nº</th>  
                                        <th class="text-start">Lot</th>  
                                        <th class="text-start">Units</th>  
                                        <th class="text-start">Quantity</th>  
                                    </tr>  
                                    <tr>  
                                        <t t-if="label.lot_id.name">  
                                            <td t-esc="label.lot_id.name"/>  
                                        </t>  
                                        <t t-else="">  
                                            <td>No Lot ID</td>  
                                        </t>  
                                        <t t-if="label.product_id.uom_id.id == 1">  
                                            <td t-esc="label.product_packaging_id.qty"  
                                                t-options="{'widget': 'float', 'precision': 3}"/>  
                                        </t>  
                                        <t t-else="">  
                                            <td>1</td>  
                                        </t>  
                                        <t t-if="label.product_id.uom_id.id == 1">  
                                            <td t-esc="label.product_packaging_id.qty * label.quantity_to_print"  
                                                t-options="{'widget': 'float', 'precision': 3}"/>  
                                        </t>  
                                        <t t-else="">  
                                            <td>0</td>  
                                        </t>  
                                        <t t-if="label.product_id.uom_id.id == 12">  
                                            <td t-esc="label.qty_done"/>  
                                        </t>  
                                        <t t-else="">  
                                            <td>0</td>  
                                        </t>  
                                    </tr>  
                                </table>  
                            </div>  
                            <div class="col-md-12">  
                                <span style="margin-right: 5%">  
                                    <span>Expiration</span>  
                                    <strong t-field="label.lot_id.expiration_date"  
                                            t-options='{"widget": "date","format": "dd/MM/yyyy"}'/>  
                                </span>  
                            </div>  
                        </div>  
                    </t>  
                </t>  
            </t>  
        </t>  
    </template>  
  
    <template id="pnt_in_picking_label_template">  
        <t t-call="web.html_container">  
            <t t-foreach="docs" t-as="doc">  
                <t t-call="report_pnt.report_pnt_in_picking_label_document" t-lang="lang"/>  
            </t>  
        </t>  
    </template>  
  
    <record id="pnt_in_picking_label_wizard_print_action" model="ir.actions.report">  
        <field name="name">Print In label</field>  
        <field name="model">in.picking.label.wizard</field>  
        <field name="report_type">qweb-pdf</field>  
        <field name="report_name">report_pnt.pnt_in_picking_label_template</field>  
        <field name="report_file">report_pnt.pnt_in_picking_label_template</field>  
        <field name="print_report_name">'Label - %s' % (object.picking_id)</field>  
        <field name="binding_type">report</field>  
        <field name="paperformat_id" ref="report_pnt.paperformat_pnt_label"/>  
    </record>  
</odoo>
```

## Ejemplos

### [Usisa v17](https://github.com/puntsistemes/usisa_odoo/commit/dad934b31376aecded97ab900f81f4aa45b7b0c0)