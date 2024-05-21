> [[Back]]

Tags: 
Status: 
Related: 

___

# Programación sin docker

> En los clientes antiguos, no tenemos `docker`, solamente ramas de `PRO` y `DEV`.

1. Creamos nuestra rama a partir de la rama PRO
2. Probamos nuestra rama, y cuando esté terminada hacemos un [[Cherrypick]] a DEV
3. Probamos nuestra rama en DEV (como si fuera un docker)
	- ssh servidor
	- git pull codigo de la rama dev
	- sudo su && systemctl stop odoo110dev && exit
	- activamos venv
	- actualizamos modulos
	- sudo su && systemctl start odoo110dev && exit
1. Devolvemos nuestros commits de DEV a PRO mediante otro [[Cherrypick]]