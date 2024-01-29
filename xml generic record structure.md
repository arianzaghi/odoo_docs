> [[Odoo Views Vistas|Back]]

Tags: #snippet #xml
Status: 
Related: 

___

# xml generic record structure


```xml
<record id="MODEL_view_TYPE" model="ir.ui.view">
  <field name="name">NAME</field>
  <field name="model">MODEL</field>
  <field name="arch" type="xml">
    <VIEW_TYPE>
      <VIEW_SPECIFICATIONS/>
    </VIEW_TYPE>
  </field>
</record>
```

- **id**: inventado, no se puede repetir. Ejemplo: `pnt_sale_form`
- **name**: igual que el id pero con puntos. Ejemplo: `pnt.sale.form`