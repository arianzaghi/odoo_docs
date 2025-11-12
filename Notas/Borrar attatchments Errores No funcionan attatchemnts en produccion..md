> [[Errores]]

Tags: 
Status: 
Related: 

___

> [!WARNING] AVISO
> A veces hay que borrar ir.asset tambien
> ```
DELETE FROM ir_asset  
WHERE (path LIKE '%.js%' OR path LIKE '%.%css%' OR path LIKE '%.xml%')  
  AND id NOT IN (  
      SELECT res_id  
      FROM ir_model_data  
      WHERE model = 'ir.asset'  
  );
> ```

# No funcionan attatchemnts en produccion
> No cargan los attatchments en producción. Después de revisar los logs vemos que no funcionan.

1. Hemos restaurado PRO a DEV
2. Siguen sin verse los attatchements
3. Ejecutamos el la siguiente orden en la bbdd que nos falla


## Desde Odoo Shell

```sh
self.env['ir.attachment'].search([('url','ilike','%.js')])
self.env['ir.attachment'].search([('url','ilike','%.js')]).unlink()

self.env['ir.attachment'].search([('url','ilike','%.cs')])
self.env['ir.attachment'].search([('url','ilike','%.cs')]).unlink()

self.env.cr.commit()
exit()
```
## Desde SQL

`psql -p 5433 DEV`
```sh
DELETE FROM ir_attachment  
WHERE  
(url ~ '^/web/(js|css)/[^/]+/.+'  
OR url ~ '^/web/(content|assets)(/[^/]+)?/[^/]+/[^/]+\.(js|css)$')  
AND id NOT IN (SELECT res_id FROM ir_model_data WHERE model = 'ir.attachment');
```

![[Pasted image 20241024094114.png]]

