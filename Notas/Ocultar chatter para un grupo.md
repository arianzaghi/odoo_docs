> [[Chatter]]

Tags: 
Status: 
Related: 

___

# Ocultar chatter para un grupo

### 1. Heredamos en nuestra vista el chatter para cambiarle la clase y ponerlo en invisible
```python
<record id="pnt_hr_employee_form_view" model="ir.ui.view">  
    <field name="name">pnt.hr.employee.form.view</field>  
    <field name="model">hr.employee</field>  
    <field name="inherit_id" ref="hr.view_employee_form"/>  
    <field name="arch" type="xml">
    
		<xpath expr="//div[@class='oe_chatter']" position="attributes">  
		    <attribute name="class">row</attribute>  
		    <attribute name="invisible">1</attribute>  
		</xpath>
		
	</field>
</record>
```


### 2. Ahora creamos un record nuevo que herede de nuestro anterior record, para asignarle a ese mismo chatter un grupo
```python
<record id="pnt_hr_employee_form_view_chatter" model="ir.ui.view">  
    <field name="name">pnt.hr.employee.form.view</field>  
    <field name="model">hr.employee</field>  
    <field name="inherit_id" ref="custom_pnt.pnt_hr_employee_form_view"/>  
    <field name="groups_id" eval="[(6, 0, [ref('custom_pnt.pnt_employees_form_access_chatter') ])]" />  
    <field name="arch" type="xml">  
  
        <xpath expr="//form//sheet" position="after">  
            <div class="oe_chatter" >  
                <field name="message_follower_ids" groups="base.group_user"/>  
                <field name="activity_ids"/>  
                <field name="message_ids"/>  
            </div>  
        </xpath>  
    </field>  
</record>
```
