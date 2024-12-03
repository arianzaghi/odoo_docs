> [[033 - Boton]]

Tags: 
Status: 
Related: 

___

# Buscar botón javascript

## Opción 1
 > Buscamos a través de Network el nombre de la ruta del boton javascript

![[Pasted image 20240902155948.png]]
1. El inspector no muestra nada de info interesante para localizar el boton
2. Hacemos click en el botón
3. Vamos a Network para ver el trafico
4. Buscamos la ruta que sale en el post en nuestro odoo

![[Pasted image 20240902160244.png]]

## Opción 2
> Estamos buscando este boton en crm.lead
![[Pasted image 20241115085058.png]]

```xml
<button name="591" string="Lost" data-hotkey="l" title="Mark as lost" type="action" invisible="type == 'lead' or not active and probability &lt; 100"/>
```

1. Vamos a `Ajustes > acciones de ventana`
2. Seleccionamos un registro cualquiera
3. Poneros en la URL el ID (`591`) y se nos abre el menu.