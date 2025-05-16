> [[Odoo Modelos|Back]]

Tags: #modelo 
Status: 
Related: [[account.move.line]]

___

# account.move

> Facturas
> Contabilidad > Clientes > Facturas

### Campo debajo de cliente
![[Pasted image 20250429112616.png]]
```xml
<?xml version='1.0' encoding='UTF-8'?>  
<odoo>  
    <record id="pnt_view_move_form" model="ir.ui.view">  
        <field name="name">pnt.account.move</field>  
        <field name="model">account.move</field>  
        <field name="inherit_id" ref="account.view_move_form"/>  
        <field name="arch" type="xml">  
            <xpath expr="//div[field[@name='partner_id']]" position="after">  
                <label string="Is Autoinvoiced" for="pnt_autoinvoice"/>  
                <field name="pnt_autoinvoice" nolabel="1"/>  
                <label string="Autoinvoice Number" for="pnt_autoinvoice_number" invisible="not pnt_autoinvoice"/>  
                <field name="pnt_autoinvoice_number" invisible="not pnt_autoinvoice" nolabel="1"/>  
            </xpath>  
        </field>  
    </record>  
</odoo>
```

## Utils

### formatLang()

```python
def formatLang(env, value, digits=None, grouping=True, monetary=False, dp=False, currency_obj=False):
```

```python
res.append({  
    'product_name': lot.product_id.display_name,  
    'quantity': formatLang(self.env, invoiced_lot_qty, dp='Product Unit of Measure'),  
    'uom_name': lot.product_uom_id.name,  
    'lot_name': lot.name,  
    # The lot id is needed by localizations to inherit the method and add custom fields on the invoice's report.  
    'lot_id': lot.id,  
})
```
