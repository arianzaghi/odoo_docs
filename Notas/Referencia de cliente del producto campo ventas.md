> [[Back]]

Tags: 
Status: 
Related: [[product.product]] [[product.template]]

___

# Referencia de cliente del producto campo ventas

![[Pasted image 20240503092233.png]]


## Modelo relacional `PntProductCustomerInfo`
```python
from odoo import models, fields  
  
  
class PntProductCustomerInfo(models.Model):  
    _name = "pnt.product.customer.info"  
    _description = "Product Customer Info"  
  
    pnt_product_id = fields.Many2one('product.template', string='Product', required=True)  
    pnt_partner_id = fields.Many2one('res.partner', string='Customer', required=True)  
    pnt_client_ref = fields.Char(string='Client ref for product')
```

## Vista del modelo relacional
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
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
  
    <record id="product_template_form_view" model="ir.ui.view">  
        <field name="name">product.template.common.form</field>  
        <field name="model">product.template</field>  
        <field name="inherit_id" ref="product.product_template_form_view" />  
        <field name="arch" type="xml">  
            <xpath expr="//page[@name='sales']/group[@name='sale']" position="after">  
                <separator string="Customers" />  
                <field name="pnt_customer_code_ids"  
                       string="Customer Codes">  
                    <tree editable="bottom">  
                        <field name="pnt_partner_id"/>  
                        <field name="pnt_client_ref"/>  
                    </tree>  
                </field>  
            </xpath>  
        </field>  
    </record>  
</odoo>
```

## Campo modelo `product.template`
```python
from odoo import models, fields, api, _  
  
  
class ProductTemplate(models.Model):  
    _inherit = "product.template"  
  
    pnt_num_loteado = fields.Char(string="Num. Loteado", size=4)  
    pnt_customer_code_ids = fields.One2many('pnt.product.customer.info', 'pnt_product_id', string='Customer Codes')  
  
    def pnt_get_client_ref(self, partner_id):  
        if partner_id:  
            for customer_productinfo in self.pnt_customer_code_ids:  
                for delivery_partner in customer_productinfo.pnt_partner_id.child_ids:  
                    if delivery_partner.id == partner_id.id:  
                        return customer_productinfo.pnt_client_ref  
        return ""
```

## Recuperar referencia de un cliente
> Con este método, asignaremos en la ficha del producto el partner_id principal, y en el pedido de venta, albarán, factura... Indicamos la dirección concreta de ese cliente.
> Al buscar la referencia estamos por tanto buscando el `partner_id` del documento origen en los `res.partner` asignados a ese cliente como direcciones de facturación
```python
def pnt_get_client_ref(self, partner_id):  
	if partner_id:  
		for customer_productinfo in self.pnt_customer_code_ids:  
			for delivery_partner in customer_productinfo.pnt_partner_id.child_ids:  
				if delivery_partner.id == partner_id.id:  
					return customer_productinfo.pnt_client_ref  
	return ""
```