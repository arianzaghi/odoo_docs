> [[BBDD]]

Tags: 
Status: 
Related: 

___

# Restaurar BBDD

```
sudo su  
pg_createcluster --locale=C.UTF-8 16 copia_temporal --start

sudo su postgres  
psql -p 5436 -d template1 < /tmp/postgresql_odoo170_1100.sql

exit

dropdb -p 5432 PRO  
createdb -p 5432 PRO  
pg_restore -p 5432 -Od PRO < /tmp/BD.dump

sudo su  
pg_dropcluster 16 copia_temporal --stop
```