> [[Buscar elementos|Back]]

Tags: 
Status: 
Related: 

___

# Botones de proyecto

> Se trata de botones que se encuentran dentro del proyecto y que permiten acceder a los recursos relacionados.
> https://github.com/puntsistemes/konery_odoo/blob/16.0/custom_pnt/models/project.py
> FTM

![[Pasted image 20240708135230.png]]

## Odoo 17
> [FTM v17](https://github.com/puntsistemes/fluidthermal_odoo/pull/10)

![[Pasted image 20240708135056.png]]

### Ejemplo de todos los botones

```python
from odoo import api, fields, models, _  
from datetime import timedelta  
  
  
class ProjectProject(models.Model):  
    _name = "project.project"  
    _inherit = 'project.project'  
  
    def _get_project_saleorder_ids(self):  
        self.ensure_one()  
        if not self.analytic_account_id:  
            return self.env['sale.order']  
        sale_order_lines = self.env['sale.order.line'].search([  
            ('analytic_distribution', '!=', False)  
        ])  
        project_sale_order_lines = sale_order_lines.filtered(  
            lambda line: str(self.analytic_account_id.id) in line.analytic_distribution  
        )  
        return self.env['sale.order'].browse(  
            project_sale_order_lines.mapped('order_id').ids  
        )  
  
    def _get_project_purchaseorder_ids(self):  
        self.ensure_one()  
        if not self.analytic_account_id:  
            return self.env['purchase.order']  
        purchase_order_lines = self.env['purchase.order.line'].search([  
            ('analytic_distribution', '!=', False)  
        ])  
        project_purchase_order_lines = purchase_order_lines.filtered(  
            lambda line: str(self.analytic_account_id.id) in line.analytic_distribution  
        )  
        return self.env['purchase.order'].browse(  
            project_purchase_order_lines.mapped('order_id').ids  
        )  
  
    def _get_outgoing_pickings(self):  
        self.ensure_one()  
        if not self.analytic_account_id:  
            return self.env['stock.picking']  
        sale_orders = self._get_project_saleorder_ids()  
        outgoing_picking_lines = self.env['stock.move'].search([  
            ('sale_line_id.order_id', 'in', sale_orders.ids)  
        ])  
        return outgoing_picking_lines.mapped('picking_id')  
  
    def _get_incoming_pickings(self):  
        self.ensure_one()  
        if not self.analytic_account_id:  
            return self.env['stock.picking']  
        purchase_orders = self._get_project_purchaseorder_ids()  
        incoming_picking_lines = self.env['stock.move'].search([  
            ('purchase_line_id.order_id', 'in', purchase_orders.ids)  
        ])  
        return incoming_picking_lines.mapped('picking_id')  
  
    def _get_production_orders(self):  
        self.ensure_one()  
        if not self.analytic_account_id:  
            return self.env['mrp.production']  
        production_orders = self.env['mrp.production'].search([  
            ('analytic_distribution', '!=', False)  
        ]).filtered(lambda prod: str(self.analytic_account_id.id) in prod.analytic_distribution)  
        return production_orders  
  
    # -------- SALE ORDERS  -------- #  
    sale_order_count = fields.Integer(  
        string='Sale Order Count',  
        compute='_compute_sale_order_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_sale_order_count(self):  
        for project in self:  
            project.sale_order_count = len(project._get_project_saleorder_ids())  
  
    def open_sale_order_ids(self):  
        self.ensure_one()  
        project_sale_orders = self._get_project_saleorder_ids()  
        return {  
            'name': 'Sale Orders',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'sale.order',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('id', 'in', project_sale_orders.ids)]  
        }  
  
    # -------- SALE INVOICES  -------- #  
    sale_invoice_count = fields.Integer(  
        string='Sale Invoice Count',  
        compute='_compute_sale_invoice_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_sale_invoice_count(self):  
        for project in self:  
            project_sale_orders = self._get_project_saleorder_ids()  
            invoices = self.env['account.move'].search([  
                ('invoice_origin', 'in', project_sale_orders.mapped('name'))  
            ])  
            project.sale_invoice_count = len(invoices)  
  
    def open_sale_invoice_ids(self):  
        self.ensure_one()  
        sales = self.env['sale.order'].search([]).filtered(lambda s: self.id in s.project_ids.ids)  
  
        return {  
            'name': 'Sale Invoice',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'account.move',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('invoice_origin', 'in', sales.mapped('name'))]  
        }  
  
    # -------- PURCHASE ORDERS  -------- #  
    purchase_order_count = fields.Integer(  
        string='Purchase Order Count',  
        compute='_compute_purchase_order_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_purchase_order_count(self):  
        for project in self:  
            if not project.analytic_account_id:  
                project.purchase_order_count = 0  
                continue  
            project.purchase_order_count = len(project._get_project_purchaseorder_ids())  
  
    def open_purchase_order_ids(self):  
        self.ensure_one()  
        project_purchase_orders = self._get_project_purchaseorder_ids()  
        return {  
            'name': 'Purchase Orders',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'purchase.order',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('id', 'in', project_purchase_orders.ids)]  
        }  
  
    # -------- PURCHASE INVOICES  -------- #  
    purchase_invoice_count = fields.Integer(  
        string='Purchase Invoice Count',  
        compute='_compute_purchase_invoice_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_purchase_invoice_count(self):  
        for project in self:  
            if not project.analytic_account_id:  
                project.purchase_invoice_count = 0  
                continue  
  
            purchase_orders = project._get_project_purchaseorder_ids()  
            invoices = self.env['account.move'].search([  
                ('invoice_origin', 'in', purchase_orders.mapped('name'))  
            ])  
            project.purchase_invoice_count = len(invoices)  
  
    def open_purchase_invoice_ids(self):  
        self.ensure_one()  
        purchase_orders = self._get_project_purchaseorder_ids()  
  
        return {  
            'name': 'Purchase Invoices',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'account.move',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('invoice_origin', 'in', purchase_orders.mapped('name'))]  
        }  
  
    # -------- OUTGOING PICKINGS  -------- #  
    outgoing_picking_count = fields.Integer(  
        string='Outgoing Picking Count',  
        compute='_compute_outgoing_picking_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_outgoing_picking_count(self):  
        for project in self:  
            if not project.analytic_account_id:  
                project.outgoing_picking_count = 0  
                continue  
            project.outgoing_picking_count = len(project._get_outgoing_pickings())  
  
    def open_outgoing_picking_ids(self):  
        self.ensure_one()  
        outgoing_pickings = self._get_outgoing_pickings()  
        return {  
            'name': 'Outgoing Pickings',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'stock.picking',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('id', 'in', outgoing_pickings.ids)]  
        }  
  
    # -------- INCOMING PICKINGS  -------- #  
    incoming_picking_count = fields.Integer(  
        string='Incoming Picking Count',  
        compute='_compute_incoming_picking_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_incoming_picking_count(self):  
        for project in self:  
            if not project.analytic_account_id:  
                project.incoming_picking_count = 0  
                continue  
            project.incoming_picking_count = len(project._get_incoming_pickings())  
  
    def open_incoming_picking_ids(self):  
        self.ensure_one()  
        incoming_pickings = self._get_incoming_pickings()  
        return {  
            'name': 'Incoming Pickings',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'stock.picking',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('id', 'in', incoming_pickings.ids)]  
        }  
  
    # -------- PRODUCTION ORDERS  -------- #  
    production_order_count = fields.Integer(  
        string='Production Order Count',  
        compute='_compute_production_order_count'  
    )  
  
    @api.depends('analytic_account_id')  
    def _compute_production_order_count(self):  
        for project in self:  
            if not project.analytic_account_id:  
                project.production_order_count = 0  
                continue  
            project.production_order_count = len(project._get_production_orders())  
  
    def open_production_order_ids(self):  
        self.ensure_one()  
        production_orders = self._get_production_orders()  
        return {  
            'name': 'Production Orders',  
            'view_type': 'form',  
            'view_mode': 'tree,form',  
            'res_model': 'mrp.production',  
            'view_id': False,  
            'type': 'ir.actions.act_window',  
            'domain': [('id', 'in', production_orders.ids)]  
        }
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<odoo>  
    <record id="pnt_project_project_form" model="ir.ui.view">  
        <field name="model">project.project</field>  
        <field name="inherit_id" ref="project.edit_project"/>  
        <field name="arch" type="xml">  
            <div name="button_box" position="inside">  
  
                <!--SALE ORDERS -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_sale_order_ids"  
                        icon="fa-tasks">  
                    <field string="Sale Orders" name="sale_order_count"  
                           widget="statinfo"/>  
                </button>  
  
                <!--SALE INVOICES-->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_sale_invoice_ids"  
                        icon="fa-tasks">  
                    <field string="Sale Invoices" name="sale_invoice_count"  
                           widget="statinfo"/>  
                </button>  
  
                <!-- PURCHASE ORDERS -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_purchase_order_ids"  
                        icon="fa-tasks">  
                    <field string="Purchase Orders" name="purchase_order_count"  
                           widget="statinfo"/>  
                </button>  
  
                <!-- PURCHASE INVOICES -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_purchase_invoice_ids"  
                        icon="fa-tasks">  
                    <field string="Purchase Invoices" name="purchase_invoice_count"  
                           widget="statinfo"/>  
                </button>  
  
                <!-- OUTGOING PICKINGS -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_outgoing_picking_ids"  
                        icon="fa-truck">  
                    <field string="Outgoing Pickings" name="outgoing_picking_count"  
                           widget="statinfo"/>  
                </button>  
  
                <!-- INCOMING PICKINGS -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_incoming_picking_ids"  
                        icon="fa-truck">  
                    <field string="Incoming Pickings" name="incoming_picking_count"  
                           widget="statinfo"/>  
                </button>  
  
                <!-- PRODUCTION ORDERS -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="open_production_order_ids"  
                        icon="fa-cogs">  
                    <field string="Production Orders" name="production_order_count"  
                           widget="statinfo"/>  
                </button>  
            </div>  
        </field>  
    </record>  
</odoo>
```

## Odoo 10
> [FTM v8](https://github.com/puntsistemes/ftm_odoo/blob/8.0/ftm_pnt/models/project_project.py)

![[Pasted image 20240708135446.png]]