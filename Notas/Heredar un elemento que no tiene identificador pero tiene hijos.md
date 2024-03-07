1> [[Informes XLM]]

Tags: 
Status: 
Related: 

___

# Heredar un elemento que no tiene identificador pero tiene hijos
Hay veces en las que queremos trabajar sobre un elemento de nuestro xml pero que no lo podemos identificar, como es este caso:

```xml
<td>  
	<span t-field="move.product_id">Customizable Desk</span>  
	<p t-if="move.description_picking != False">  
		<span t-field="move.description_picking">Description on transfer</span>  
	</p>  
</td>
```

- En este caso, queremos ocultar el td entero
- Solución: Buscamos un td en función a su hijo
## Solución
```xml
<xpath expr="//td[span[@t-field='move.product_id']]" position="attributes">
    <attribute name="invisible">1</attribute>
</xpath>
```

## Ejemplo

>[Ingelev](https://github.com/puntsistemes/ingelev_odoo/pull/3/files)