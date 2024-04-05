> [[Herencia]]

Tags: 
Status: 
Related: 

___

# Herencia de un xpath en otro template

## Contamos con:
- Informe A (Original)
- Informe B (Modifica a Informe A usando xpath)
- Informe C (Nuestro informe, queremos cambiar el xpath de Informe B)

### Informe A

```xml

```

### Informe B
```xml
<!-- INFORME B -->
<template id="stock_report_delivery_has_serial_move_line_inherit_delivery" inherit_id="stock.stock_report_delivery_has_serial_move_line">  
    <xpath expr="//td[@name='move_line_lot_qty_done']" position="after">  
        <td t-if="has_hs_code"><span t-field="move_line.product_id.hs_code"/></td>  
    </xpath>  
</template>
```

### Informe C

```xml
<!-- INFORME C -->
<template id="pnt_report_delivery_document_has_serial_move_line"  
	inherit_id="delivery.stock_report_delivery_has_serial_move_line_inherit_delivery">  
	
    <td t-if="has_hs_code" position="attributes">  
        <attribute name="t-if" add="False" separator=" and "/>  
    </td>  
  
</template>
```

## Ejemplos

