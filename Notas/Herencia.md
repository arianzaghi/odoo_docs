> [[Odoo Views Vistas|Back]]

Tags: 
Status: 
Related: 

___
# Herencia

Podemos utilizar 3 formas para heredar de una vista para modificarla:

- Elemento `xpath` con atributo `expr` aplicado al template correspondiente
```xml
<xpath expr="page[@name='pg']/group[@name='gp']/field" position="inside">
  <field name="description"/>
</xpath>
```

- Elemento `field` con atributo `name`, busca el primer `field` con el mismo atributo `name`. El resto de atributos son ignorados durante la búsqueda
```xml
<field name="res_id" position="after"/>
```

- Cualquier otro elemento: busca el primer elemento con el mismo nombre y atributos idénticos (ignorando los atributos `position` y `version`)
```xml
<div name="name" position="replace">
  <div name="name2">
    <field name="name2"/>
  </div>
</div>
```

**Position**
- `inside (default)`
	El contenido se añade dentro del elemento matcheado en el xml
	
- `replace`
	El contenido reemplaza el elemento encontrado.
	
- `after`
	El contenido de la herencia se añade después del elemento buscado
	
- `before`
	El contenido de la herencia se añade antes del elemento buscado

- `attributes`
	El contenido de la herencia debería ser un elemento `attribute` con atributo `name` y un cuerpo opcional
	- Si `attribute` tiene contenido, se crea un nuevo atributo con el nombre indicado por su `name` en el nodo coincidente, y se le asigna el texto del elemento `attribute` como valor.
	- Si el elemento `attribute` no tiene contenido, el atributo con el nombre indicado por su `name` se elimina del nodo coincidente. Si dicho atributo no existe, se genera un error.
