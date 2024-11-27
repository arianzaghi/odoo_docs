> [[Vista Pivot]]

Tags: 
Status: 
Related: 

___

# Modelo intermedio para pivot, pasar columnas no relacionales a filas

> El objetivo es crear un modelo relacional a `Hoja de calculo` que permita almacenar datos numéricos específicos. Hacemos esto para poder visualizar luego la tabla `pivot` de `Hoja de calculo` viendo como filas los datos numéricos (como si fueran un row).

## Antes

1. **Pivot Original**
	En este modelo guardamos el `empleado`, la `fecha` y campos de tipo `float` que almacenan el dato de las horas de cada tipo que se han realizado.
	Queremos poder ver estos campos numéricos como filas en la tabla `pivot`, pero como no son campos por los que se pueda agrupar, **NO PODEMOS**

> ![[Pasted image 20241127133243.png]]

## Después

1. **Pivot Nueva**
	Creamos este nuevo modelo en el que guardaremos el tipo de la hora a la que hacemos referencia, y el valor.
	Este modelo solo almacena 1 dato, incluyendo su tipo y su valor. El resto de campos, solo sirven para relacionarse con el modelo anterior.
	Como ahora el `tipo de hora` es selection, y el valor esta en otro campo `float`, ahora **SI** que podemos mostrar los valores en las filas

![[Pivot intermedia]]

![[Pasted image 20241127132737.png]]




