> [[Stat button]]

Tags: 
Status: 
Related: 

___

# Stat button - Boton para abrir partes de horas de un proyecto timesheets

> Stat Button en project.project que nos permite abrir una vista de los partes de horas de un proyecto para aquellos usuarios que tienen permisos 
> [https://github.com/puntsistemes/fluidthermal_odoo/pull/14/fileshttps://github.com/puntsistemes/fluidthermal_odoo/pull/15/files](FluidThermal - 17)

![[Pasted image 20250224105601.png]]
![[Pasted image 20250224105628.png]]

```python
from odoo import api, fields, models, _  
from odoo.exceptions import AccessError  
  
  
class ProjectProject(models.Model):  
    _name = "project.project"  
    _inherit = ["project.project", "pnt.search.sql.mixin"]  
  
    pnt_has_timesheets = fields.Boolean(  
        string='Has Timesheets',  
        compute='_compute_pnt_has_timesheets',  
        store=True,  
    )  
  
    pnt_timesheet_count = fields.Integer(  
        string='Timesheet Count',  
        compute='_compute_pnt_timesheet_count',  
        store=False,  
    )  
  
    @api.depends('timesheet_ids')  
    def _compute_pnt_timesheet_count(self):  
        for project in self:  
            project.pnt_timesheet_count = self.env['account.analytic.line'].search_count(  
                [('project_id', '=', project.id),  
                 ('is_timesheet', '=', True)])  
  
    @api.depends('timesheet_ids')  
    def _compute_pnt_has_timesheets(self):  
        for project in self:  
            project.pnt_has_timesheets = bool(  
                self.env['account.analytic.line'].search_count(  
                    [('project_id', '=', project.id),  
                     ('is_timesheet', '=', True)]  
                )  
            )  
  
    def action_open_timesheets_pnt(self):  
        if not self.env.user.has_group('hr_timesheet.group_hr_timesheet_user'):  
            raise AccessError(_("You don't have enough permissions to access Timesheets."))  
        domain = [('project_id', '=', self.id)]  
        if not self.env.user.has_group('hr_timesheet.group_timesheet_manager'):  
            domain.append(('user_id', '=', self.env.user.id))  
        return {  
            'type': 'ir.actions.act_window',  
            'name': 'Partes de Horas',  
            'res_model': 'account.analytic.line',  
            'view_mode': 'tree,form',  
            'domain': domain,  
            'context': {'default_project_id': self.id},  
        }
```


```xml<?xml version="1.0" encoding="UTF-8" ?>  
<odoo>  
    <record id="pnt_project_project_form" model="ir.ui.view">  
        <field name="model">project.project</field>  
        <field name="inherit_id" ref="project.edit_project"/>  
        <field name="arch" type="xml">  
            <div name="button_box" position="inside">
				<!-- TIMESHEETS -->  
				<button class="oe_inline oe_stat_button"  
				        type="object"  
				        name="action_open_timesheets_pnt"  
				        icon="fa-clock-o">  
				    <field string="Timesheets" name="pnt_timesheet_count"  
				           widget="statinfo"/>  
				</button>
            </div>  
        </field>  
    </record>  
</odoo>
```