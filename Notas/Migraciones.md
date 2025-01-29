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


## Pruebas con singularu

1. Hacer `update all` de la version que vamos a migrar
2. Comentar lineas clave de `.bash_aliases` reiniciar terminal o `source bash_aliases`
```sh
	database_odoo "${db_local}" &>/dev/null    # Comentar para migraciones  
	_database_odoo_remove_assets "${db_local}" # Comentar para migraciones
	```
3. Comentar el addons path excepto los repos de odoo (core, enterprise)
4. Hacemos lista de modulos que no son del core para ver cual podemos borrar. Preguntamos a consultor
5. Mandamos la bbdd a odoo
	`python3 <(curl -s https://yograde.odoo.com/upgradetest -j $(nproc) -d ORIGEN_PRO -t 15.0`
1. Entramos al docker de postgres
	`docker container exec -it postgres bash`
6. Instalamos paquetes
```sh
apt update &&
apt install 'y ''no'install'recommends ''no'install 
```