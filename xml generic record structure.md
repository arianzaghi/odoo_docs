> [[Back]]

Tags: #snippet #xml
Status: 
Related: 

___

# xml generic record structure


```xml
<record id="" model="ir.ui.view">  
    <field name="name">name</field>  
    <field name="model">model.name</field>  
    <field name="arch" type="xml">  
         
    </field>  
</record>
```

- **id**: inventado, no se puede repetir. Ejemplo: `pnt_sale_form`
- **name**: igual que el id pero con puntos. Ejemplo: `pnt.sale.form`