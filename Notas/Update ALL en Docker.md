> [[Dockers Odoo]]

Tags: 
Status: 
Related: 

___

# Update ALL en Docker

```sh
cp -r /opt/odoo/odoo180dev/src/ /opt/odoo/odoo180dev/src_backup
```

```sh
docker container exec -i odoo180dev_postgres pg_dump -U odoo -Fc -Z3 -O -d DEV > /opt/odoo/odoo180dev/DEV.dump
```

```sh
cd /opt/odoo/odoo180dev/src
./git_update 18.0
```

```sh
docker compose -f /opt/odoo/odoo180dev/compose_odoo.yml run --rm odoo180dev --stop-after-init --no-xmlrpc --log-level=info --i18n-overwrite -d DEV -u all
```