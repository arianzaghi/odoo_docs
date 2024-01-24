> [[Odoo Views]]

Tags: #xml 
Status: 
Related: 

___

# Search filter tree view


```python
<record id="view_helpdesk_ticker_search" model="ir.ui.view">  
    <field name="name">view.helpdesk_ticket</field>  
    <field name="model">helpdesk.ticket</field>  
    <field name="arch" type="xml">  
         <search string="Tickets">  
  
             <field name="name"/>  
             <field name="user_id"/>  
             <field name="assigned"/>  
             <field name="date"/>  
  
             <filter string="User assigned" name="date" domain="[('user_id', '!=', False)]"/>  
             <filter string="Assigned" name="date" domain="[('assigned', '=', True)]"/>  
             <filter string="No Date" name="date" domain="[('date', '!=', False)]"/>  
  
  
             <group string="Group By" name="groupby">  
                 <filter name="user_id_groupby" string ="User" context="{'group_by': 'user_id'}"/>  
                 <filter name="date_groupby" string="Date" context="{'group_by': 'date'}"/>  
             </group>  
         </search>  
    </field>  
</record>
```


