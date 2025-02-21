> [[Back]]

Tags: 
Status: 
Related: 

___

# Migraciones



> [!Info] Versiones para migrar
> Solo se pueden migrar las versiones enterprise
> Solo se pueden migrar las 3 ultimas versiones
> Solo se puede migrar `enterprise`. Le tienes que mandar la bbdd para que te la migren
## Proceso General

> https://upgrade.odoo.com/

### 1. Modificamos `.bash_aliases`
1. Comentamos las lineas que eliminan el código `enterprise` de la `bbdd`
![[Pasted image 20250220132512.png]]
2. Recargamos el fichero bash aliases
```sh
cd && sources .bash_aliases
```
### Borrar modulos no instalados desde odoo en local
![[Pasted image 20250221113643.png]]
### 2. Hacer `update all` de la version que vamos a migrar en nuestro local
	1. Abrimos `Pycharm` en version de nuestro cliente
	2. Actualizamos / Clonamos el repositorio del cliente
	3. Lanzamos `git_log` en el cliente y lo traemos al local
	4. Lanzamos `git_client_mirror`
	5. Lanzamos `git_update {{13.0}}`
	6. Clonamos `bbdd` de `PRO`
	7. Arrancamos odoo haciendo `update all`
```sh
-c /opt/sources/odoo130/conf/dilesa.conf -d DILESA_PRO -u all --i18n-overwrite --no-xmlrpc -stop-after-init
```

### 3. Hacemos un listado de los modulos que no son de odoo
1. Modificamos el script `dev-tools/scripting/module_analyzer_stats.py` para aplicar nuestra configuración	
	- **CUSTOMER**: El nombre del cliente para mostrar en los resultados.
	- **DATABASE**: El nombre de la base de datos de Odoo.
	- **PASSWORD**: La contraseña de la base de datos de Odoo (Postgres).
	- **PORT**: El puerto de PostgreSQL (usualmente 5432).
	- **PATH_MAIN**: La ruta donde está instalada Odoo.
	- **DIR_CUSTOM**: El directorio de módulos personalizados (si es necesario).
2. Lanzamos el script desde el cliente

### 4. Actualizamos la BBDD

1. Entramos al `docker` de `postgres`
```sh
docker container exec -it postgres bash
```
1. Instalamos paqueteria para lanzar el comando
```sh
apt update && apt install -y --no-install-recommends --no-install-suggests rsync openssh-client curl ca-certificates python3
```
1. Iniciamos sesion como usuario `odoo`, o sino lo creamos
```sh
adduser odoo
su odoo
mkdir 14_15
```
1. Lanzamos comando para actualizar la bbdd
```sh
python3 <(curl -s https://upgrade.odoo.com/upgrade) [tipo_de_migracion] -j $(nproc) -d [base_de_datos_a_migrar] -t [version_destino]

#Ejemplo
python3 <(curl -s https://upgrade.odoo.com/upgrade) test -j $(nproc) -d DILESA_PRO -t 14.0
```

## Dilesa
## Pruebas con singularu

1. Hacer `update all` de la version que vamos a migrar
2. Comentar lineas clave de `.bash_aliases` reiniciar terminal o `source bash_aliases`
```sh
	database_odoo "${db_local}" &>/dev/null    # Comentar para migraciones  
	_database_odoo_remove_assets "${db_local}" # Comentar para migraciones
```
1. Comentar el addons path excepto los repos de odoo (core, enterprise)
2. Hacemos lista de modulos que no son del core para ver cual podemos borrar. Preguntamos a consultor
3. Mandamos la bbdd a odoo
	`python3 <(curl -s https://yograde.odoo.com/upgradetest -j $(nproc) -d ORIGEN_PRO -t 15.0`
1. Entramos al docker de postgres
	`docker container exec -it postgres bash`
6. Instalamos paquetes
```sh
apt update &&
apt install 'y ''no'install'recommends ''no'install 
```