> [[Modificaciones comunes Informes XML]]

Tags: 
Status: 
Related: 

___

# quitar producto y solo dejar descripcion PV, FRA

FRA
```xml
<!-- Quitar producto de la tabla y mostrar solo descripción -->  
<xpath expr="//td[@name='account_invoice_line_name']//span[@t-field='line.name']" position="replace">  
    <t t-raw="(line.name or '').replace(line.product_id.name or '', '').strip().replace('\n', '&lt;br/&gt;')"/>  
</xpath>
```

PV
```xml
<!-- Quitar producto mostrar solo descripcion en tbala -->  
<xpath expr="//td[@name='td_name']//span[@t-field='line.name']" position="replace">  
    <t t-raw="(line.name or '').replace(line.product_id.name or '', '').strip().replace('\n', '&lt;br/&gt;')"/>  
</xpath>
```