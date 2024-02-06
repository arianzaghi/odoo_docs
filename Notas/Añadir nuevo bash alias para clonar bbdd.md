> [[Workflow Punt]]

Tags: 
Status: 
Related: 
Back
___

# Añadir nuevo alias para clonar bbdd

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