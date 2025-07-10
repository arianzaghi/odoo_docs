> [[100 - Dev-tools]]

Tags: 
Status: 
Related: 

___

# Script launcher miquel

Buenos días,  
  
He subido a addons-standard un módulo para lanzar scripts desde Odoo,  
[https://github.com/puntsistemes/addons-standard_odoo/tree/17.0/script_launcher_pnt](https://github.com/puntsistemes/addons-standard_odoo/tree/17.0/script_launcher_pnt
Es necesario que el usuario esté en este grupo: Lanzador de comandos

![[Pasted image 20250127090133.png]]
Se crea un Script con nombre, descripción y la ruta donde se encuentra el fichero de script en el servidor de Odoo (o local)

Se puede lanzar el script desde el wizard lanzador o desde el Script.  
Una vez ejecutado devuelve los resultados y se guardan en un historial de logs.![[Pasted image 20250127090138.png]]
![[Pasted image 20250127090142.png]]Se puede usar para reiniciar servicios (jasper, vpn, cups, etc), restaurar BD de PRO a DEV, o cualquier cosa que se pueda lanzar desde un script.  
  
Espero que os pueda servir!