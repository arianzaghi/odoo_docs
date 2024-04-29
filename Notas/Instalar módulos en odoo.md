> [[Back]]

Tags: 
Status: 
Related: 

___

# Instalar módulos en odoo

## Requisitos

- Nombre del repositorio 
	`stock-logistics-warehouse`
- Nombre del modulo
	`stock_mts_mto_rule`
- Link del repo (opcional)
	` https://github.com/OCA/stock-logistics-warehouse/tree/17.0/stock_mts_mto_rule`

## Instalación

1. Navegamos a la carpeta `oca` del cliente
	`odoo170/src/addons-custom/cliente/oca`

2. Ejecutamos la siguiente instrucción
	`ln -sf ../../REPOSITORIO/MODULO .`

3. Lanzamos client_mirror
	`./git_client_mirror.sh cliente.txt`

> [!IMPORTANT] Importante
> La ruta que estamos poniendo en el paso 2 NO existe en local (no se auto completará mientras la escribimos). Esa ruta existe dentro del servidor.

> En el paso 2 creamos un acceso directo que no existe en nuestro equipo local. Tras la ejecución de `git_client_mirror`, se instala en nuestro equipo el módulo


> [!DANGER] Recuerda
> Después de instalar el módulo hay que activarlo, tanto en el docker de pruebas como en PRO


## Adicionalmente

1. Comprobamos que en nuestro local en `/opt/sources/odoo170/src/` exista el modulo que estamos instalando (`bank_payment`), y que este actualizado (`git pull`)
2. Creamos enlace en el servidor, git log y git mirror en nuestro local
3. añadir linea en nuestro config