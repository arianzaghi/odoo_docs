> [[Contextos]]

Tags: 
Status: 
Related: 

___

# Leer contexto desde una vista pasado a través de una acción

> Estamos en una vista y queremos leer un contexto que se ha pasado desde una acción para saber si ocultar o no un campo

```xml
<field name='pnt_name' column_invisible="context.get('variable') == 'valor')"/>
```