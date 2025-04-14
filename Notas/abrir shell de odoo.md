> [[Back]]

Tags: 
Status: 
Related: 

___

# Abrir shell de odoo (mientras esta arrancado)

## En producción
```bash
/opt/odoo/odoo170/src/core/odoo-bin shell -c /opt/odoo/odoo170/conf/rankia.conf -d PRO --xmlrpc-port 9090
```

## En local

> Desde la terminal del `Pycharm`:

```sh
/opt/sources/odoo170/src/core/odoo-bin shell -c /opt/sources/odoo170/conf/aidimme.conf -d aidimme_221 --xmlrpc-port 9090
```