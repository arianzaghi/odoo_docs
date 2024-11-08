> [[<button> Boton]]

Tags: 
Status: 
Related: 

___

# quitar boton de crear nuevo registro en modelo

```xml
<form create="false">
<tree create="false">
```

```xml
<record id="pnt_daily_extra_hour_calc_view_form" model="ir.ui.view">  
    <field name="name">pnt.daily.extra.hour.calc.view.form</field>  
    <field name="model">pnt.daily.extra.hour.calc</field>  
    <field name="arch" type="xml">  
        <form string="Hours calc" class="o_sale_order" create="false">
```