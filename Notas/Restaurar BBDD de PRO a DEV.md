> [[BBDD Servidor]]

Tags: 
Status: 
Related: 

___

# Restaurar BBDD PRO a DEV

## Clonar Pro en Dev

### Borrar BBDD Dev
```
dropdb -p {{puerto_DEV}} {{BBDD_DEV}}
```

### Volver a crear y restaurar datos
```bash
time (createdb -p {{puerto_dev}} {{BBDD_DEV}}) && time (pg_dump -p {{puerto_pro}} -Fc -Z4 -Od {{BBDD_PRO}} | pg_restore -p {{puerto_dev}} -Od {{BBDD_DEV}})
```

`PUERTO_DEV`: Puerto de dev
`BBDD_DEV`: Nombre de bbdd de dev
`PUERTO_PRO`: Puerto de pro
`BBDD_PRO`: Nombre de bbdd de pro

**Ejemplo**
```bash
time (createdb -p 5433 DEV) && time (pg_dump -p 5432 -Fc -Z4 -Od PRO | pg_restore -p 5433 -Od DEV)
```

## Configurar Nueva BBDD Dev
Después de clonar la bbdd de pro a dev, necesitamos ejecutar en `DEV` lo siguiente

### Conexión a Dev desde el servidor
```bash
psql -p {{PUERTO_DEV}} {{NOMBRE_BBDD}}
```
**Ejemplo**
```bash
psql -p 5433 DEV
```

### Configuración de Dev
```sql
UPDATE ir_cron SET active=false;
UPDATE ir_mail_server SET active=false;
UPDATE res_company SET sii_enabled=false;
SET client_min_messages TO WARNING;
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
INSERT INTO "ir_config_parameter" ("key", "value")
VALUES
('report.url', 'http://127.0.0.1:8070'),
('web.base.url', 'https://meysser-dev.odoo.puntsistemes.cloud/:8070'),
('database.uuid', uuid_generate_v1()),
('database.secret', uuid_generate_v4())
ON CONFLICT ("key") DO
UPDATE SET "value" = EXCLUDED."value";
DELETE FROM ir_config_parameter WHERE key IN ('database.enterprise_code', 'odoo_ocn.project_id', 'mail_mobile.enable_ocn');
```

Esto lo encontramos en el conf del servidor.
```sql
# Educonsul
('report.url', 'http://127.0.0.1:8070'),
('web.base.url', 'http://odoo-dev.sek.net/:8070'),

#Meysser
('report.url', 'http://127.0.0.1:8070'),
('web.base.url', 'https://meysser-dev.odoo.puntsistemes.cloud/:8070'),

#Punt dev
('report.url', 'http://0.0.0.1:62001'),
('web.base.url', 'https://odoo-dev.puntsistemes.com/:62001'),

#Redit
('report.url', 'http://127.0.0.1:62000'),
('web.base.url', 'https://redit-dev.puntsistemes.cloud/:62001'),

#Coelbe
('report.url', 'http://127.0.0.1:62001'),
('web.base.url', 'https://coelbe-dev.puntsistemes.cloud/:62001'),

#Palacio
('report.url', 'http://127.0.0.1:62001'),
('web.base.url', 'https://odoo-dev.palcongres-vlc.com/:62001'),

#Som Energia
('report.url', 'http://127.0.0.1:62001'),
('web.base.url', 'https://odoocifdev.somenergia.coop/:62001'),
```


cat odoo140dev/conf/odoo140dev.conf
- Comprobamos el puerto http_port debe coincidir con 
- ('report.url', 'http://127.0.0.1:8073'),
- ('web.base.url', 'http://127.0.0.1:8073'),

('web.base.url', 'http://127.0.0.1:8073'),
- URL de acceso a instalación de dev. Si es la misma, indicamos el puerto.
- (Igual que accederríamos en internet)

