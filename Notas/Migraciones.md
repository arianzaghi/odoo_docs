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

## Dilesa 13 a 15
> M21120333632356

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



```sh
('account_menu_invoice_refund.menu_action_invoice_out_tree', 271, 'Accounting > Customers > Invoices / Credit Notes', 415):  
Traceback (most recent call last):  
  File "/tmp/tmp4vez2lfo/migrations/base/tests/test_mock_crawl.py", line 259, in crawl_menu  
   self.mock_action(action_vals)  
  File "/tmp/tmp4vez2lfo/migrations/base/tests/test_mock_crawl.py", line 272, in mock_action  
   return self.mock_act_window(action)  
  File "/tmp/tmp4vez2lfo/migrations/base/tests/test_mock_crawl.py", line 356, in mock_act_window  
   views = get_views(  
  File "/home/odoo/src/odoo/15.0/odoo/models.py", line 1640, in load_views  
   result['fields_views'] = {  
  File "/home/odoo/src/odoo/15.0/odoo/models.py", line 1641, in <dictcomp>  
   v_type: self.fields_view_get(v_id, v_type if v_type != 'list' else 'tree',  
  File "/home/odoo/src/odoo/15.0/addons/web/models/models.py", line 249, in fields_view_get  
   r = super().fields_view_get(view_id, view_type, toolbar, submenu)  
  File "/home/odoo/src/odoo/15.0/odoo/models.py", line 1724, in fields_view_get  
   result = self._fields_view_get(view_id=view_id, view_type=view_type, toolbar=toolbar, submenu=submenu)  
  File "/home/odoo/src/odoo/15.0/odoo/models.py", line 1686, in _fields_view_get  
   result['arch'] = view.get_combined_arch()  
  File "/home/odoo/src/odoo/15.0/odoo/addons/base/models/ir_ui_view.py", line 963, in get_combined_arch  
   return etree.tostring(self._get_combined_arch(), encoding='unicode')  
  File "/home/odoo/src/odoo/15.0/addons/website/models/ir_ui_view.py", line 549, in _get_combined_arch  
   root = super()._get_combined_arch()  
  File "/home/odoo/src/odoo/15.0/odoo/addons/base/models/ir_ui_view.py", line 993, in _get_combined_arch  
   arch = root.with_prefetch(tree_views._prefetch_ids)._combine(hierarchy)  
  File "/home/odoo/src/odoo/15.0/odoo/addons/base/models/ir_ui_view.py", line 934, in _combine  
   combined_arch = view.apply_inheritance_specs(combined_arch, arch)  
  File "/home/odoo/src/odoo/15.0/odoo/addons/base/models/ir_ui_view.py", line 871, in apply_inheritance_specs  
   self._raise_view_error(str(e), specs_tree)  
  File "/home/odoo/src/odoo/15.0/odoo/addons/base/models/ir_ui_view.py", line 748, in _raise_view_error  
   raise err from from_exception  
ValueError: Element '<field name="amount_untaxed">' cannot be located in parent view  
  
  
  
2025-02-20 15:13:58,631 6138 INFO db_2586734 odoo.upgrade.testing: Starting IntegrityCase.test_check ...   
2025-02-20 15:13:58,632 6138 INFO db_2586734 odoo.upgrade.testing: skipped IntegrityCase.test_check   
2025-02-20 15:13:58,632 6138 INFO db_2586734 odoo.upgrade.base.tests.test_module_state: Starting TestModuleState.test_check ...   
2025-02-20 15:13:58,633 6138 INFO db_2586734 odoo.upgrade.testing: Calling TestModuleState.check   
2025-02-20 15:13:58,634 6138 INFO db_2586734 odoo.upgrade.testing: Starting IntegrityCase.test_check ...   
2025-02-20 15:13:58,635 6138 INFO db_2586734 odoo.upgrade.testing: skipped IntegrityCase.test_check   
2025-02-20 15:13:58,635 6138 INFO db_2586734 odoo.upgrade.base.tests.test_ensure_has_pk: Starting TestTablesHavePK.test_check ...   
2025-02-20 15:13:58,636 6138 INFO db_2586734 odoo.upgrade.testing: Calling TestTablesHavePK.check   
2025-02-20 15:13:58,643 6138 INFO db_2586734 odoo.upgrade.testing: Starting IntegrityCase.test_check ...   
2025-02-20 15:13:58,644 6138 INFO db_2586734 odoo.upgrade.testing: skipped IntegrityCase.test_check   
2025-02-20 15:13:58,644 6138 INFO db_2586734 odoo.upgrade.stock.tests.test_uom_consistency: Starting TestUoMConsistencyChanges.test_check ...   
2025-02-20 15:13:58,645 6138 INFO db_2586734 odoo.upgrade.testing: Calling TestUoMConsistencyChanges.check   
2025-02-20 15:13:58,684 6138 INFO db_2586734 odoo.upgrade.testing: Starting IntegrityCase.test_check ...   
2025-02-20 15:13:58,685 6138 INFO db_2586734 odoo.upgrade.testing: skipped IntegrityCase.test_check   
2025-02-20 15:13:58,685 6138 INFO db_2586734 odoo.upgrade.stock.tests.test_on_hand_quantity: Starting TestOnHandQuantityUnchanged.test_check ...   
2025-02-20 15:13:58,686 6138 INFO db_2586734 odoo.upgrade.testing: Calling TestOnHandQuantityUnchanged.check   
2025-02-20 15:13:58,917 6138 INFO db_2586734 odoo.service.server: 15 post-tests in 34.01s, 25057 queries   
2025-02-20 15:13:58,918 6138 ERROR db_2586734 odoo.tests.runner: 1 failed, 0 error(s) of 15 tests when loading database 'db_2586734'   
2025-02-20 15:13:58,918 6138 INFO db_2586734 odoo.service.server: Initiating shutdown   
2025-02-20 15:13:58,918 6138 INFO db_2586734 odoo.service.server: Hit CTRL-C again or send a second signal to force the shutdown.   
2025-02-20 15:13:59,321 6138 INFO db_2586734 odoo.sql_db: ConnectionPool(used=0/count=0/max=64): Closed 2 connections   
[ERROR]::Error during the upgrade: command execution has failed with the error code 1  
2025-02-20 03:14:42 ERROR: The upgrade request has failed
```