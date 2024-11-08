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
- clonar src desde home de @odoo
	`cp -r ~/odoo160dev/src ~/odoo160dev/src_backup`
- Hacemos copia de la BBDD por si acaso
	`pg_dump -p {{puerto}} DEV > /tmp/DEV_{{fecha}}.dump`
- Actualizamos deade `odoo170dev/src/`
  `./git_update {{branch}}`
	- Necesitamos usuario y token para descargar enterprise
- Activamos venv
	`source venv/bin/activate`
- Update ALL
```sh
python3 /opt/odoo/odoo{{version}}{{modo}}/src/core/odoo-bin -c /opt/odoo/odoo{{version}}{{modo}}/conf/odoo{{version}}{{modo}}.conf --stop-after-init --i18n-overwrite '--log level=info' --no-xmlrpc -d {{database_name}} -u all
```


## PRO

Si han pasado varios dias desde el update all de dev, en vez de hacer update all en pro, copiamos el src de dev, ya que puede que hayan habido actualizaciones en ese periodo, entonces si hacemos UPDATE ALL en PRO, no quedarían igual.

- Paramos el servidor
	`sudo su`
	`systemctl stop odoo160`
- Hacemos una copia del src de pro por si acaso
	`cp -r ~/odoo160/src ~/odoo160/src_backup`
- Ponemos el `src` de DEV en PRO
	`cp -r ~/odoo160dev/src ~/odoo160/`
- Actualizamos la BBDD de PRO con Update ALL
```sh
python3 /opt/odoo/odoo160/src/core/odoo-bin -c /opt/odoo/odoo{{version}}{{modo}}/conf/odoo160.conf --stop-after-init --i18n-overwrite '--log level=info' --no-xmlrpc -d PRO -u all
```
- Arrancamos 

> [!DANGER] IMPORTANTE
> Si el cliente NO USA DOCKER, tenemos que cambiar a la rama de PRO


backup de src de prod (con mv)
cp src_dev a src_pro
En los clientes que no funcionan con docker, necesitamos establecer la rama src>addons_custom>git checkout 16.0 (main)