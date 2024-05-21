> [[Server]]

Tags: 
Status: 
Related: 

___

# Compartir carpetas entre local y servidor

> Necesario cuando queremos copiar algún directorio o fichero desde servidor cliente hasta máquina local.

```bash
rsync -aP {{CLIENTE}}:/opt/odoo/odoo{{VERSION}}/{{PATH1}} :/opt/odoo/odoo{{VERSION}}/{{PATH2}} {{LOCAL_DEST_PATH}}
```

- {{CLIENTE}}: ssh del cliente
- {{VERSION}}: 140, 170dev....
- {{PATH1}}, {{PATH2}}: Rutas que queremos mover del servidor a local
- {{LOCAL_DEST_PATH}}: Ruta destino en local

**Ejemplo**
```bash
rsync -aP zubilabs:/opt/odoo/odoo140/src/zubi_events :/opt/odoo/odoo140/src/addons-zubilabs ~/sources/odoo140/src/
```

