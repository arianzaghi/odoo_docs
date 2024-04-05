> [[Informes XLM]]

Tags: 
Status: 
Related: 

___

# Formatear decimales en unidades reporte

```xml
<t t-esc="my_number" t-options="{'widget': 'float', 'precision': 2}"/>
```


> [!EXAMPLE] 1.005,00
> ```xml
>t-options="{'widget': 'float', 'precision': 2}"
>``` 

**Para xpath**
```xml
<attribute name="t-options">  
	{'widget': 'float', 'precision': 2}
</attribute>
```


> [!EXAMPLE] 1005
> ```xml
>t-options="{'widget': 'float', 'precision': 0}"
>``` 
