> [[Workflow Punt|Back]]
# Pasos para la configuración del Odoo de un cliente en nuestro equipo local



## 1. Dentro del servidor cliente:

1. Nos conectamos mediante [[SSH]]. Los clientes se encuentran en [[.bash_aliases]]
   ```
   ssh "client"
	```
   
2. Navegamos a la ruta del proyecto odoo
	```
	cd path/to/odoo/src
	```
	
3. Ejecutamos [[git_log.sh]] recuperar listado de repositorios de producción y la versión de cada uno.
	```
	./git_log.sh
	```
 ^29de65
4. Copiamos el output del comando anterior. Lo usaremos más adelante para rellenar [[Odoo clonar cliente#^8b17fc|'client.txt']]

## 2. En nuestro local odoo Docker

> **Ruta proyecto en Docker:** */opt/sources/odooXXX/*
> **Ruta proyecto en Local:** */home/user/sources/odooXXX/*

<br>

### 2.1 Descargamos repositorio del cliente

> Dentro de la consola del Docker (@odoo)

5. Navegamos al directorio de repositorios dentro de la carpeta de odoo
	```
	cd src/addons_custom
	```

6. Clonamos repositorio del cliente, o lo actualizamos

```
git clone <client_repo>
or
git pull
```

### 2.2 Actualizar versiones de los módulos y dependencias

7. Creamos 'client.txt' en el **src** del proyecto odoo
   ```
	touch 'client.txt'
	```
8. Pegamos el output de [[Odoo clonar cliente#^29de65|./git_log.sh]] en 'client.txt' ^8b17fc
9. Ejecutamos [[git_client_mirror.sh]] para la actualización de módulos

	```
	./git_client_mirror.sh 'client.txt'
	```

10. Copiamos output del comando anterior que contiene el listado de [[addons-path]]

### 2.3 Fichero de configuración de Odoo

^d519ad

11. Creamos fichero conf del cliente duplicando 'odoo.conf'
```
	cp conf/odoo.conf conf/client.conf
```
12. Pegamos los [[addons-path]] en 'client.conf'
