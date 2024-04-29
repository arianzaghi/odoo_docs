> [[Impresion de informes]]

Tags: #informe
Status: 
Related: [[Paperformat]]

___

# Imprimir informe con dos paperformat distintos

- Contamos con 2 `paperformat`, el por defecto (A4) y un nuevo `paperformat` en horizontal (A4_Horizontal)
- Queremos imprimir un mismo informe desde 2 botones, y que cada botón tenga su propio `paperformat`

## Creamos nuevo botón de acción

Nuevo botón tendrá indicado el `paperformat` que vamos a usar (A4_Horizontal)

```xml
<record id="pnt_action_report_saleorder" model="ir.actions.report">  
    <field name="name">Albaran Horizontal</field>  
    <field name="model">stock.picking</field>  
    <field name="report_type">qweb-pdf</field>  
    <field name="report_name">report_pnt.pnt_report_deliveryslip</field>  
    <field name="print_report_name">Nombre Documento</field>  
    <field name="binding_model_id" ref="stock.model_stock_picking"/>  
    <field name="binding_type">report</field>  
    <field name="paperformat_id" ref="report_pnt.pnt_custom_horizontal_paperformat"/>  
</record>  
```

## Creamos nuevo template para el reporte

```xml
<template id="pnt_report_deliveryslip">  
    <t t-foreach="docs" t-as="o">  
        <t t-call="stock.report_delivery_document" t-lang="o._get_report_lang()"/>  
    </t>  
</template>
```

## Conclusión

### #todo 

Terminamos con:
- 2 Botones de accion
	- El del core (sin paperformat indicado)
	- El nuestro nuevo (con paperformat indicado)
- 2 Templates de invocación
	- El el del core
	- El nuestro nuevo
- 1 Único Informe (original)