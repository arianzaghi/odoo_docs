> [[Modificaciones comunes XLM]]

Tags: 
Status: 
Related: 

___

# Formatear fecha reporte

```xml
<p t-field="o.scheduled_date" t-options='{"widget": "date","format": "dd/MM/yyyy"}'/>
```


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
