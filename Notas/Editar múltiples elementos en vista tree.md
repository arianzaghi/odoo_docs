> [[Vista List o Tree - Listado]]

Tags: 
Status: 
Related: 

___

# Editar múltiples elementos en vista tree

`<tree multi_edit="1" string="Issues">`

```xml
<record id="sport_issue_view_tree" model="ir.ui.view">
	<field name="name">sport.issue.view.tree</field>
	<field name="model">sport.issue</field>
	<field name="arch" type="xml">
		<tree multi_edit="1" string="Issues">
			<field name="sequence" widget="handle"/>
			<field name="name"/>
			<field name="date" optional="show"/>
			<field name="user_id" optional="hide"/>
			<field name="state"/>
		</tree>
	</field>
</record>
```