Tags: 
Status: 
Related: 

___

# dev-tools MOC

## Estructura

### helpers

- [[.bash_aliases]]
	Aqui se están las entradas de los bash aliases para clonar bbdd de clientes
- [[config]]
	Y aquí están las entradas para hacer ssh en los servidores cliente

### install_development
- [[odoo.conf]]
	Fichero de configuración de ejemplo para los clientes.
	Solo es necesario modificar el addons-path [[Odoo clonar cliente#^d519ad|(Obtener addons-path)]]

### scaffolding
Aquí encontramos ejemplos de los módulos `custom_pnt` y `report_pnt` para crearlos en clientes que todavía no los tienen

### scripting
Aquí se encuentran los scripts principales para la clonación de clientes

- [[git_log.sh]]
- [[git_update.sh]]
- [[git_client_mirror.sh]]

## Añadir nuevo alias para clonar bbdd

> `dev-tools > helpers > .bash_aliases`

1. Copiamos una entrada existente (están en el final del fichero) y modificamos los parámetros acorde al cliente.

```python
alias joares_pro='_get_client_db joares 5432 PRO JOARES_PRO 14'
```

	- joares_pro: Nombre del alias que ejecutaremos en terminal
	- 5432: Puerto del servidor (5433 para dev y 5432 para pro)
	- PRO: Nombre de la bbdd en el servidor del cliente
	- JOARES_PRO: Nombre de la bbdd en nuestro equipo cuando lo clonemos
	- 14: Parametro opcional para indicar la versión de odoo del cliente

2. Ordenamos alfabeticamente las entradas
	- Seleccionamos todos los bash aliases
	- `Click derecho > string manipulation > Repeat - sort lines > ok`

## Añadir alias para hacer ssh a servidor cliente





## [[Bash y scripts]]