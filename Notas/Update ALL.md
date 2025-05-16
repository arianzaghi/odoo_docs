> [[090  - Servidor gestion]]

Tags: 
Status: 
Related: 

___

# Update ALL

> Esta operación consiste en:
>1. Actualizar todos los módulos y repositorios del proyecto
>2. Actualizar BBDD (comando `update all`)

> [!WARNING] IMPORTANTE
> Primero lo hacemos en `DEV` y si todo funciona bien en `PRO`.
> **PRO TIP:** Cuando `DEV` esté ok, clonamos el `src` en `PRO` para tener exactamente el mismo commit de git
> y evitamos que si ha pasado mucho tiempo entre los dos update all, no haya commits entre medio.

## Update ALL en DEV

> Como usuario `odoo`

1. Paramos el servidor
```sh
	sudo su
	systemctl stop odoo{{branch}}dev
```

2. Clonamos el src de `DEV`
```sh
cp -r /opt/odoo/odoo{{branch}}dev/src /opt/odoo/odoo{{branch}}dev/src_backup
```

3. Hacemos copia de la BBDD por si acaso
```sh
pg_dump -p {{puerto}} DEV > /tmp/DEV_{{fecha}}.dump
```

4. Actualizamos repositorios de dev
> Necesitamos usuario y token para descargar enterprise
```sh
cd /opt/odoo/odoo{{branch}}dev/src
./git_update {{branch}}`
```

5. Activamos venv
```sh
source venv/bin/activate
```

6. Lanzamos Update ALL
```sh
python3 /opt/odoo/odoo{{version}}{{modo}}/src/core/odoo-bin -c /opt/odoo/odoo{{version}}{{modo}}/conf/odoo{{version}}{{modo}}.conf --stop-after-init --i18n-overwrite '--log level=info' --no-xmlrpc -d {{database_name}} -u all
```
## Update ALL en PRO

> **Recuerda:** Si han pasado varios dias desde el update all de dev, en vez de hacer update all en pro, copiamos el src de dev, ya que puede que hayan habido actualizaciones en ese periodo, entonces si hacemos UPDATE ALL en PRO, no quedarían igual.

1. Paramos el servidor
```sh
sudo su
systemctl stop odoo{{version}}dev
```
2. Hacemos una copia del src de pro por si acaso
```sh
mv /opt/odoo/odoo160/src /opt/odoo/odoo160/src_backup
```
3. Ponemos el `src` de DEV en PRO
```sh
cp -r /opt/odoo/odoo160dev/src /opt/odoo/odoo160/
```
4. Activamos el venv
```sh
source venv/bin/activate
```
4. Actualizamos la BBDD de PRO con Update ALL
```sh
python3 /opt/odoo/odoo160/src/core/odoo-bin -c /opt/odoo/odoo{{version}}{{modo}}/conf/odoo160.conf --stop-after-init --i18n-overwrite '--log level=info' --no-xmlrpc -d PRO -u all
```
5. Arrancamos `DEV` y testeamos

> [!DANGER] IMPORTANTE
> Si el cliente NO USA DOCKER, tenemos que cambiar a la rama de PRO
> `src>addons_custom>git checkout 16.0 (main)`