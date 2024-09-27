> [[Vista List o Tree - Listado]]

Tags: #xml 
Status: 
Related: 

___

# Search filter tree view
> Queremos añadir en nuestra vista tree filtros como los siguientes:
![[Pasted image 20240904163131.png]]

## Creamos una vista para el `search view`
```python
<record id="{{MODEL_}}_view_search" model="ir.ui.view">  
    <field name="name">{{MODEL.}}.view.search</field>  
    <field name="model">{{MODEL.}}</field>  
    <field name="arch" type="xml">  
         <search string="{{SEARCH_STRING}}">  
  
             <field name="pnt_petitioner_id"/>  
             <field name="pnt_petition_date"/>  
             <field name="pnt_petition_status"/>  
             <field name="pnt_is_daily_petition"/>  
  
             <filter string="User assigned" name="date" domain="[('user_id', '!=', False)]"/>  
             <filter string="Assigned" name="date" domain="[('assigned', '=', True)]"/>  
             <filter string="No Date" name="date" domain="[('date', '!=', False)]"/>  
  
			  # CAMPOS PARA AGRUPAR (Recuadro rojo)
             <group string="Group By" name="groupby">  
                 <filter name="user_id_groupby" string ="User" context="{'group_by': 'user_id'}"/>  
                 <filter name="date_groupby" string="Date" context="{'group_by': 'date'}"/>  
             </group>  
         </search>  
    </field>  
</record>
```

## Referenciamos el `search view` a la accion del modelo
```python
<field name="search_view_id" ref="view_pnt_petition_search"/>

# LO AÑADIMOS
<record id="pnt_petition_action" model="ir.actions.act_window">  
    <field name="name">Peticiones</field>  
    <field name="res_model">pnt.petition</field>  
    <field name="view_mode">tree,form</field>  
    <field name="search_view_id" ref="view_pnt_petition_search"/>  # Lo añadimos aqui
    <field name="help" type="html">  
        <p class="o_view_nocontent_smiling_face">No items created.</p>  
    </field>  
</record>
```


## Ejemplos
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

[[Añadir filtro de referencia de cliente]]