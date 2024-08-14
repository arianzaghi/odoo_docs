> [[Modulos core de odoo]]

Tags: 
Status: 
Related: 

___

# product.template

## Form view

**Template to inherit from `product.template` form view**
```xml
<record id="pnt_product_template_form_view" model="ir.ui.view">  
    <field name="model">product.template</field>  
    <field name="name">pnt.product.template.form.view</field>  
    <field name="inherit_id" ref="product.product_template_only_form_view"/>  
    <field name="arch" type="xml">  
        <xpath expr="//field[@name='product_tag_ids']" position="after">  
            <field string='Num. Loteado' name="pnt_num_loteado"/>  
        </xpath>  
    </field>  
</record>
```