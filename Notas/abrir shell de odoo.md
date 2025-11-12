an be > [[090  - Servidor gestion]]

Tags: 
Status: 
Related: 

___

# Abrir shell de odoo (mientras esta arrancado)

## En producción
```bash
# Palacio
/opt/odoo/odoo170/src/core/odoo-bin shell -c /opt/odoo/odoo170/conf/palacio.conf -d PRO --xmlrpc-port 9090
# Rankia
/opt/odoo/odoo170/src/core/odoo-bin shell -c /opt/odoo/odoo170/conf/rankia.conf -d PRO --xmlrpc-port 9090
# Meysser
/opt/odoo/odoo140dev/src/core/odoo-bin shell -c /opt/odoo/odoo140dev/conf/odoo140dev.conf -d DEV --xmlrpc-port 9090
```

## En local

> Desde la terminal del `Pycharm`:

```sh
/opt/sources/odoo170/src/core/odoo-bin shell -c /opt/sources/odoo170/conf/aidimme.conf -d aidimme_221 --xmlrpc-port 9090
/opt/sources/odoo170/src/core/odoo-bin shell -c /opt/sources/odoo170/conf/hegoplac.conf -d HEGOPLAC_PRO --xmlrpc-port 9090
/opt/sources/odoo170/src/core/odoo-bin shell -c /opt/sources/odoo170/conf/palacio.conf -d PALACIO_17_PRO --xmlrpc-port 9090
/opt/sources/odoo140/src/core/odoo-bin shell -c /opt/sources/odoo140/conf/meysser.conf -d MEYSSER_PRO --xmlrpc-port 9090

```

## En maquinas con Docker

```sh
docker exec -it {{odoo180dev}} /opt/odoo/src/core/odoo-bin shell -c /opt/odoo/conf/odoo.conf -d DEV --xmlrpc-port 9090
```