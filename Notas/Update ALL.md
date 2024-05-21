> [[Server]]

Tags: 
Status: 
Related: 

___

# Update ALL
Esta operación consiste en actualizar todos los módulos y repositorios del proyecto.
Primero la hacemos en DEV, y si todo funciona bien en PRO.

## DEV
 
- Paramos el servidor
	`sudo su`
	`systemctl stop odoo160dev`
- clonar src
	`cp -r ~/odoo160dev/src ~/odoo160dev/src_backup`
- Hacemos copia de la BBDD por si acaso
	`pg_dump -p {{puerto}} DEV > /tmp/DEV_{{fecha}}.dump`
- Actualizamos
  `./git_update {{branch}}`
	- Necesitamos usuario y token para descargar enterprise
- Activamos venv
	`source venv/bin/activate`
- Update ALL
	`python /opt/odoo/odoo{{version}}{{modo}}/src/core/odoo-bin -c /opt/odoo/odoo{{version}}{{modo}}/conf/odoo{{version}}{{modo}}.conf --stop-after-init --i18n-overwrite '--log level=info' --no-xmlrpc -d {{database_name}} -u all


## PRO

Si han pasado varios dias desde el update all de dev, en vez de hacer update all en pro, copiamos el src de dev.

- Paramos el servidor
	`sudo su`
	`systemctl stop odoo160dev`
- clonar src
	`cp -r ~/odoo160dev/src ~/odoo160dev/src_backup`
- Hacemos copia de la BBDD por si acaso
	`pg_dump -p {{puerto}} DEV > /tmp/DEV_{{fecha}}.dump`
- Arrancamos 

backup de src de prod (con mv)
cp src_dev a src_pro
En los clientes que no funcionan con docker, necesitamos establecer la rama src>addons_custom>git checkout 16.0 (main)