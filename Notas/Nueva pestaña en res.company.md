> [[res.company]]

Tags: 
Status: 
Related: 

___

# Nueva pestaña en res.company

![[Pasted image 20240610165600.png]]

```xml
<odoo>  
    <record id="view_company_form" model="ir.ui.view">  
        <field name="model">res.company</field>  
        <field name="inherit_id" ref="base.view_company_form" />  
        <field name="arch" type="xml">  
            <notebook position="inside">  
                <page string="Sanitary registry" name="sanitary_registry_page">  
                    <group string="Sanitary registry" name="sanitary_registry">  
                        <field name="pnt_sanitary_registry_ids" string="Sanitary registry ">  
                            <tree>  
                                <field name="pnt_product_sector_id"/>  
                                <field name="pnt_registry_number"/>  
                            </tree>  
                        </field>  
                    </group>  
                </page>  
            </notebook>  
        </field>  
    </record>  
</odoo>
```