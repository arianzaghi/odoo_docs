> [[Back]]

Tags: 
Status: 
Related: 

___

# Añadir un nuevo dominio al nginx de una instalación de odoo

1. Modificamos `/etc/nginx/sites-available/{{dominio_existente}}.conf`
2. Añadiremos en este fichero de conf el nuevo dominio que queremos añadir
	- De esta manera, los dos dominios apuntarán a la misma web 

**Ejemplos con varios dominios:**
- Punt v16
- Educonsul