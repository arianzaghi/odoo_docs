> [[Modificaciones comunes XLM]]

Tags: 
Status: 
Related: 

___

# Formatear fecha reporte
## Copy Paste `t-options`

> [!EXAMPLE] 13/02/2024
> ```xml
>t-options='{"widget": "date","format": "dd/MM/yyyy"}'
>``` 

> [!EXAMPLE] 13 Feb 2024
> ```xml
>t-options='{"widget": "date","format": "dd MMMM yyyy"}'
>``` 

> [!EXAMPLE] 13/02/24
> ```xml
>t-options='{"widget": "date","format": "dd/MM/yy"}'
>``` 

## Copy Paste `<attribute>`

> [!EXAMPLE] 13/02/2024
> ```xml
><attribute name="t-options">{"widget": "date","format": "dd/MM/yyyy"}</attribute>
>``` 

> [!EXAMPLE] 13 Feb 2024
> ```xml
> <attribute name="t-options">{"widget": "date","format": "dd MMMM yyyy"}</attribute>>
> ``` 

> [!EXAMPLE] 13/02/24
> ```xml
><attribute name="t-options">{"widget": "date","format": "dd/MM/yy"}</attribute>>
>``` 

## Ejemplos
> **Modificación desde el formulario**
```xml
<p t-field="o.scheduled_date" t-options='{"widget": "date","format": "dd/MM/yyyy"}'/>
```

> **Modificación desde XPATH**
```xml
<xpath expr="//div[@name='usuarios']" position="attributes">
	<attribute name="t-options">{"widget": "date","format": "dd/MM/yyyy"}</attribute>
</xpath>
```
