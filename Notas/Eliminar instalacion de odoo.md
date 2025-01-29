> [[Server]]

Tags: 
Status: 
Related: 

___

# Eliminar odoo

> Proceso para eliminar instalaciones de odoo que ya no están en uso.

> [!Warning] Aviso
> Esto hay que hacerlo con root, porque hay que manejar servicios y como `odoo` no tenemos permisos.

**Elementos a eliminar:**
1. Servicios
2. Postgres
3. Crons
4. Nginx
5. Directorio Instalación
6. Certificado

## 1. Servicios

- Buscamos el servicio de odoo
```
ls /etc.systemd/system/odoo170MIG.service
```
- Paramos el servicio
```
systemctl stop odoo170MIG
```
- Deshabilitamos el servicio
```
disable odoo170MIG
```
- Borramos el fichero de configuracion
```
rm -rf /etc.systemd/system/odoo170MIG.service
```

## 2. Postgres

> Tenemos que desactivar primero y luego borrar los clusters

> [!INFO] Localizar cluster del odoo
> Para saber a quien pertenece el cluster, vamos al archivo config de odoo y buscamos el puerto

`pg_lsclusters` para ver los clusters. Localizamos el asociado al odoo que queremos eliminar.
![[Pasted image 20250129153000.png]]


> [!DANGER] CUIDADO
> El comando `systemctl stop postgres` para **todas** las instalaciones

**Paramos nuestro cluster**
```sh
pg_ctlcluster 16 odoo170MIG_5436 stop
```

**Eliminar nuestro cluster**
```sh
pg_dropcluster --stop 16 odoo170MIG_5436
# Este comando lo para antes de eliminarlo también
```

**Borrar carpeta adicional creada por nosotros**
```sh
rm -rf /etc/postgres/16/odoo170MIG_5436
```

## 3. Cron

> Borrar tareas programadas
```sh
crontab -l

crontab -u odoo -e
```

## 4. Nginx

> Eliminamos las configuraciones de nginx
```sh
ls cd /etc/nginx/sites-enabled
rm odoov17mig.palcongres-vlc.com.conf

ls cd /etc/nginx/sites-available
rm odoov17mig.palcongres-vlc.com.conf
```

**Comprobar que todo funciona bien**
```sh
nginx -t
```

**Refrescar archivos de conexion**
```sh
systemctl reload nginx
```

## 5. Directorio instalación y backups

> Borramos la carpeta del odoo
```sh
rm -rf odoo170MIG
```

> Eliminamos los backups de esa instalación
```sh
ls /opt/backups/odoo/

rm -rf /opt/backups/odoo/*odoo170MIG*.log`
```

> [!INFO] INFO
> Se realizan copias de seguridad diarias a las horas:
> - **8:00**
> - **11:00**
> - **14:00**
> - **17:00**
> - **20:00**


## 6. Certificado
> Ejecutamos `certbot` y seleccionamos la opción para eliminar los certificados de la instalación vieja

```sh
certbot delete
```

![[Pasted image 20250129163000.png]]
