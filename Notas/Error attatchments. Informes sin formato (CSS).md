> [[Errores]]

Tags: 
Status: 
Related: 

___

# Error los informes se imprimen sin formato (CSS)

> Los informes de odoo PRO o DEV, no cargan los attatchemtns

![[Pasted image 20240613162354.png]]
> Hay que configurar el campo `report.url` desde odoo web

1. Ajustes > Técnico > Parámetros del sistema
2. Configuramos `report.url`
	- Ponemos el puerto del `conf` del servidor
	- La url sigue siendo `https://127.0.0.1`
1. Buscamos el puerto en `http_port`
	- `cat /opt/odoo/odoo170/conf/odoo170dev.conf | grep port`
2. Reiniciamos el servidor