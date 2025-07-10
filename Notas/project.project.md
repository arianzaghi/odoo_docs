> [[Odoo Modelos]]

Tags: 
Status: 
Related: 

___

# project.project

## Herencia FORM
![[Pasted image 20250512122805.png]]
```xml
<record id="pnt_view_task_form2_inherited" model="ir.ui.view">  
    <field name="name">pnt.view.task.form2.inherited</field>  
    <field name="model">project.task</field>  
    <field name="inherit_id" ref="hr_timesheet.view_task_form2_inherited"/>  
    <field name="arch" type="xml">  
        <xpath expr="//div[field[@name='allocated_hours']]" position="after">  
             <field name="pnt_cost"/>  
        </xpath>  
    </field>  
</record>
```