> [[Back]]

Tags: 
Status: 
Related: 

___

# abrir linea de listado tree one2many

```xml
<record id="pnt_hr_attendance_view_form" model="ir.ui.view">  
    <field name="model">hr.attendance</field>  
    <field name="inherit_id" ref="hr_attendance.hr_attendance_view_form"/>  
    <field name="arch" type="xml">
    
    <xpath expr="//separator" position="before">
		<field name="pnt_petition_ids" readonly="False" nolabel="1">  
		    <tree>  
		        <field name="..."/> 
		        <button name="action_open_form"  
		                type="object"  
		                string="Open"  
		                icon="fa-external-link"/>  
			</tree>
		</field>
	<xpath/>
<record/>
```

```python
class PntPetition(models.Model):  
    _name = "pnt.petition"  
    _inherit = ["mail.thread", "mail.activity.mixin"]  
    _description = "Petitions of extra hours."  
    _rec_name = "pnt_petitioner_id"  
    _order = "pnt_petition_date"

def action_open_form(self):  
    """
    Opens the form view of the current record in full screen.
    """  
    return {  
        "type": "ir.actions.act_window",  
        "res_model": "pnt.petition",  
        "view_mode": "form",  
        "res_id": self.id,  
        "target": "current",  # Abre en pantalla completa  
    }
```
