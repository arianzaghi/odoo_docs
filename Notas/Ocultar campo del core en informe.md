> [[Modificaciones comunes XLM]]

Tags: 
Status: 
Related: 

___

# Ocultar campo del core en informe

Añadimos el siguiente atributo al elemento que queremos ocultar
```xml
<attribute name="t-if" add="False" separator=" and "/>
```

## Ejemplo

**Queremos ocultar**
```xml
<div class="col-auto col-3 mw-100 mb-2" t-if="o.partner_id.ref" name="customer_code">  
    <strong>Customer Code:</strong>  
    <p class="m-0" t-field="o.partner_id.ref"/>  
</div>
```

**Ocultamos usando**
```xml
<xpath expr="//div[@name='customer_code']" position="attributes">  
    <attribute name="t-if" add="False" separator=" and "/>  
</xpath>
```