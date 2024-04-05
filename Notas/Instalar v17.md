> [[Server]]

Tags: 
Status: 
Related: 

___

# Instalar v17

- Comprobsmos los DNS
	`DNS Checker` https://dnschecker.org/
- Buscamos la passwords del servidor cliente
	`Odoo > Passwords > Ubuntu > Cliente`
- Nos conectamos al servidor nuevo (NO POR ALIAS)
	`root@{{IP}}`
- Creamos el script de instalación
	`touch /temp/install.sh`
- Copiamos el contenido del script 
	script: `install_production_standard.sh`
	ubicación: `github devtools rama main`
- Damos permisos de ejecución al script
	`chmod +x /tmp/install.sh`
- 
	dns prod y dev
	- dev SI
	- usuario y token
- 
- Crear 2 entradas de passwords (dev y prod) ==> ODOO bundle

> [!IMPORTANT]
> Antes de salir del server (despues de la instalacion)  añadir alias para ssh en cliente

