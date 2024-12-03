> [[050 - Security]]

Tags: 
Status: 
Related: 

___
# Grupos
[[Buscar grupos de permisos]]
## Crear nuevo grupo
`security/`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
<odoo>  
    <record model="ir.module.category" id="base.module_category_human_resources_employees">  
        <field name="sequence">10</field>  
    </record>  
  
    <record id="group_product_price_block_pnt" model="res.groups">  
        <field name="name">Product Price Blocker</field>  
        <field name="category_id" ref="base.module_category_human_resources_employees"/>  
        <field name="implied_ids" eval="[(6, 0, [ref('base.group_user')])]"/>  
        <field name="comment">The user will be able to access all requests and approve/refuse them.</field>  
    </record>  
</odoo>  
  
</odoo>
```

## Ejemplos
### [Palacio v17 attendance_pnt/security]()