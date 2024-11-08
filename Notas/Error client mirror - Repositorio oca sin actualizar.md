> [[git_client_mirror.sh]]

Tags: 
Status: 
Related: 

___

# Error client mirror - Repo oca sin actualizar

>**Problema:** Cuando arrancamos odoo, nos salen errores por los diferentes modelos diciendo que hay campos definidos en BBDD que no se encuentran en el código.
>**Motivo:** Un módulo (oca) ha sido instalado y esta presente en BBDD pero no se encuentra en el equipo local. Por tanto, nos da error de campo perdido

1. Identificamos los módulos que están causando el error 
	- Lanzamos odoo con `-u custom_pnt`
		![[Pasted image 20240718094721.png]]
	- Buscamos a qué modulo pertenece ese modelo que da error
		`sale-workflow`
1. Navegamos al módulo para comprobar que está actualizado y que el modelo se encuentra dentro. Sino, git pull
	`ls -la /opt/sources/odoo170/src/sale-workflow`
	`cd /opt/sources/odoo170/src/sale-workflow && git pull`
1. Ponemos enlace simbólico al modelo en la carpeta oca del cliente
	`cd /opt/sources/odoo170/src/addons-oca/fluidthermal`
	`ln -sf ../../sale-workflow/sale_layout_category_hide_detail .`
	
	![[Pasted image 20240718102148.png]]
	