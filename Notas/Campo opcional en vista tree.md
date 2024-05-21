> [[Vista List o Tree - Listado]]

Tags: 
Status: 
Related: 

___

# Campo opcional en vista tree

> Queremos añadir un campo en las lineas de la vista tree que se pueda mostrar/ocultar desde el menú (tres puntos) de la derecha

```xml
<field name="..." optional="show"/>
```

```xml
<tree string="Tickets" multi_edit="1" sample="1">
	<field name="team_id" invisible="1" readonly="1"/>
	<field name="display_name" string="Ticket Name" readonly="1"/>
	<field name="partner_id" optional="show"/>
	<field name="user_id" optional="show" widget="many2one_avatar_user"/>
	<field name="ticket_type_id" optional="hide"/>
	<field name="priority" optional="hide"/>
	<field name="tag_ids" optional="hide" widget="many2many_tags" options="{'color_field': 'color'}"/>
	<field name="activity_ids" widget="list_activity" optional="show"/>
	<field name="stage_id" optional="show" readonly="1"/>
	<field name="company_id" groups="base.group_multi_company" optional="show" readonly="1"/>
</tree> 
```