> [[Errores]]

Tags: 
Status: 
Related: 

___

# No funcionan attatchemnts en produccion

> No cargan los attatchments en producción. Después de revisar los logs vemos que no funcionan.

1. Hemos restaurado PRO a DEV
2. Siguen sin verse los attatchements
3. Ejecutamos el la siguiente orden en la bbdd que nos falla


`psql -p 5433 DEV`
```sh
DELETE FROM ir_attachment  
WHERE  
(url ~ '^/web/(js|css)/[^/]+/.+'  
OR url ~ '^/web/(content|assets)(/[^/]+)?/[^/]+/[^/]+\.(js|css)$')  
AND id NOT IN (SELECT res_id FROM ir_model_data WHERE model = 'ir.attachment');
```

![[Pasted image 20241024094114.png]]

