> [[Migraciones]]

Tags: 
Status: 
Related: 

___

# Hacer un migrations

> En mi caso concreto, he necesitado hacer este proceso porque después de una actualización de código tengo que ejecutar una consulta sql para pasar datos de un campo a otro (del nuevo al viejo).

1. Declaramos un directorio migrations y dentro otro directorio con la version
	1. Asignamos numero de versión por el que va a pasar el modulo cuando se actualice, con el script
	2. Incrementamos la versión del manifest también
		1. **Por ejemplo:** 
			- manifest "version": "17.0.1.0.3",-> "version": "17.0.1.0.4"
			- directorio migrations version: 17.0.1.0.4
	3. Dentro de la segunda carpeta ('17.0.1.0.4') 