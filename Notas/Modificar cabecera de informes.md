> [[Mover o modificar elementos de informe]]

Tags: 
Status: 
Related: 

___

# Modificar cabecera de informes
Para cambiar la cabecera de los informes, heredamos de la plantilla `external_layout_striped`

> [!DANGER] Importante
> Esta cabecera se aplica a todos los informes


![[Pasted image 20240214152730.png]]


```xml
<?xml version="1.0" encoding="utf-8"?>
 <odoo>
     <template id="pnt_external_layout_bold_header" inherit_id="web.external_layout_bold">
     </template>
 </odoo>
```