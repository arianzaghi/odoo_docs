> [[<xpath>]]

Tags: 
Status: 
Related: 

___

# Mover elemento de la vista del core

> Tenemos un group en la vista del `core` y queremos moverla de sitio fuera del page. Utilizaremos **`attribute='move'`**

![[Pasted image 20250120115337.png]]

**`group original`**
```xml
<group string="Marketing" name="categorization">  
    <field name="company_id"  
        groups="base.group_multi_company"  
        options="{'no_create': True}"/>  
    <field name="campaign_id" options="{'create_name_field': 'title'}"/>  
    <field name="medium_id"/>  
    <field name="source_id"/>  
    <field name="referred"/>  
</group>
```

**Lo movemos al lado de `pnt_tariff`**

```xml
# Ruta de donde queremos posicionar el elemento
<xpath expr="//group[@name='pnt_tariff']" position="after">  
    # Ruta del elemento que quermeos mover
    <xpath expr="//group[@name='categorization']" position="move"/>  
</xpath>
```