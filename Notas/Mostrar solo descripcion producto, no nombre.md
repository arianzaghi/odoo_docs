> [[Mover o modificar elementos de informe]]

Tags: 
Status: 
Related: 

___

# Mostrar solo descripcion producto, no nombre

```xml
<!-- Quitar producto mostrar solo descripcion en tbala -->  
<xpath expr="//td[@name='td_name']//span[@t-field='line.name']" position="replace">  
    <t t-raw="(line.name or '').replace(line.product_id.name or '', '').strip().replace('\n', '&lt;br/&gt;')"/>  
</xpath>
```