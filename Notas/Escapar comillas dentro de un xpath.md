> [[<xpath>]]

Tags: 
Status: 
Related: 

___

# Escapar comillas dentro de un xpath

> Cuando intentamos poner un texto con comillas dentro de un xpath
> `<div t-if="o.picking_type_id.code == 'outgoing' and o.carrier_id"`
> El xpath nos da problemas.
```xml
&quot;
```

## Solucion

### mal
```xml
<xpath expr="//div[@t-if='o.picking_type_id.code == 'outgoing' and o.carrier_id']/div[@t-if]" position="attributes">  
    <attribute name="t-if">o.picking_type_id.code == 'outgoing' or o.carrier_id</attribute>  
</xpath>
```

### bien
```xml
<xpath expr="//div[@t-if='o.picking_type_id.code == &quot;outgoing&quot; and o.carrier_id']/div[@t-if]" position="attributes">  
    <attribute name="t-if">o.picking_type_id.code == 'outgoing' or o.carrier_id</attribute>  
</xpath>
```

![[Pasted image 20250513092124.png]]
![[Pasted image 20250513092131.png]]