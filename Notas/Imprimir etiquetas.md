> [[Impresion de informes]]

Tags: 
Status: 
Related: 

___

# Imprimir etiquetas
## Documento etiqueta
```xml
<template id="{{pnt_package_barcode_document}}">
	<t t-call="web.basic_layout">  
	    <t t-foreach="docs" t-as="o">
		    ...
		</t>
	</t>
</template>
```

## Botón de impresión
```xml
<record id="pnt_package_barcode_action" model="ir.actions.report">  
    <field name="name">{{Nombre boton impresion}}</field>  
    # Modelo destino y de datos
    <field name="model">stock.quant.package</field>  
    <field name="report_type">qweb-pdf</field>
    # Nombre del documento de la etiqueta
    <field name="report_name">{{report_pnt}}.{{pnt_package_barcode_document}}</field>  
    <field name="report_file">{{report_pnt}}.{{pnt_package_barcode_document}}</field>  
    # Modelo donde se muestra el boton de impresion
    <field name="binding_model_id" ref="{{stock.model_stock_quant_package}}"/>  
    <field name="binding_type">report</field>  
</record>
```

## Ejemplos 

### 1. Signes: Etiquetas lotes
- Botón de imprimir etiquetas desde `stock.picking` 
- Imprime una etiqueta por linea en `stock.move.line`
- [Signes_49701](https://github.com/puntsistemes/bona-gent_odoo/pull/44/commits/8378d1e09d1d3c4e87bd098ae3f39e6e1860696e#diff-8b857d45237d44ffe08a8959e63446c96c803486e5256a39dd6be3b994280403)
### 2. Etiquetas desde wizard
- [[Wizard Impresion Etiqueta Rellenando Campos]]
- [[Wizard impresión Etiquetas desde Albarán con Lotes]]