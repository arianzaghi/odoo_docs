> [[Back]]

Tags: 
Status: 
Related: 

___

# Ocultar accion de duplicar

**TREE**
```xml
<!-- Ocultar el botón de duplicar en las vistas de árbol -->  
<record id="pnt_crm_lead_view_tree_oppor_inherit" model="ir.ui.view">  
    <field name="name">crm.lead.view.tree.oppor.inherit</field>  
    <field name="model">crm.lead</field>  
    <field name="inherit_id" ref="crm.crm_case_tree_view_oppor"/>  
    <field name="arch" type="xml">  
        <xpath expr="//tree" position="attributes">  
            <attribute name="duplicate">false</attribute>  
        </xpath>    </field></record>
```

**FORM**
```xml
<!-- Ocultar el botón de duplicar -->  
<xpath expr="//form" position="attributes">  
    <attribute name="duplicate">false</attribute>  
</xpath>
```