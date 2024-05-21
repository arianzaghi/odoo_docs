> [[Modificaciones comunes XLM]]

Tags: 
Status: 
Related: 

___
# Formatear decimales en unidades reporte
## Copy Paste `t-options`

> [!EXAMPLE] 1005
> ```xml
>t-options="{'widget': 'float', 'precision': 0}"
>``` 

> [!EXAMPLE] 1005,00
> ```xml
>t-options="{'widget': 'float', 'precision': 2}"
>``` 

## Copy Paste `<attribute>`

> [!EXAMPLE] 1005,00
> ```xml
> <attribute name="t-options">{'widget': 'float', 'precision': 2}</attribute>
> ``` 

> [!EXAMPLE] 1005
> ```xml
><attribute name="t-options">{'widget': 'float', 'precision': 0}</attribute>
>``` 

## Ejemplos
> **Modificación desde el formulario**
```xml
<t t-esc="my_number" t-options="{'widget': 'float', 'precision': 2}"/>
```

> **Modificación desde XPATH**
```xml
<attribute name="t-options">  
	{'widget': 'float', 'precision': 2}
</attribute>
```
