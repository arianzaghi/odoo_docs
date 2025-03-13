> [[Stat button]]

Tags: 
Status: 
Related: 

___

# Stat button: Botón para abrir documentos de un proyecto

> Stat Button en project.project que nos permite abrir una vista de los documentos de un proyecto para aquellos usuarios que tienen permisos 
> [https://github.com/puntsistemes/fluidthermal_odoo/pull/14/fileshttps://github.com/puntsistemes/fluidthermal_odoo/pull/14/files](FluidThermal - 17)

![[Pasted image 20250224093604.png]]
![[Pasted image 20250224093625.png]]


```python
class ProjectProject(models.Model):  
    _name = "project.project"  
    _inherit = ["project.project", "pnt.search.sql.mixin"]  
  
    pnt_has_documents = fields.Boolean(compute="_compute_pnt_has_documents", store=True)  
    pnt_document_count = fields.Integer(  
        string='Document Count',  
        compute='_compute_pnt_document_count',  
        store=False,  
    )  
  
    @api.depends('message_ids')  
    def _compute_pnt_document_count(self):  
        for project in self:  
            project.pnt_document_count = self.env['documents.document'].search_count([('project_id', '=', project.id)])  
  
    @api.depends('pnt_document_count')  
    def _compute_pnt_has_documents(self):  
        for project in self:  
            project.pnt_has_documents = project.pnt_document_count > 0  
  
  
    def action_open_documents_pnt(self):  
        if not self.env.user.has_group('documents.group_documents_user'):  
            raise AccessError(_("You don't have enough permissions to access Project Documents."))  
        return {  
            'type': 'ir.actions.act_window',  
            'name': 'Documentos',  
            'res_model': 'documents.document',  
            'view_mode': 'tree,form',  
            'domain': [('project_id', '=', self.id)],  
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
                <!-- DOCUMENTS -->  
                <button class="oe_inline oe_stat_button"  
                        type="object"  
                        name="action_open_documents_pnt"  
                        icon="fa-file">  
                    <field string="Documents" name="pnt_document_count"  
                           widget="statinfo"/>  
                </button>  
            </div>  
        </field>  
    </record>  
</odoo>
```