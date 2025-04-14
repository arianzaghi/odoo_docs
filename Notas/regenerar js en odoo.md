> [[Back]]

Tags: 
Status: 
Related: 

___

# regenerar js en odoo

1. Nos conectamos al shell de odoo dev
2. Borramos los adjuntos
```
self.env['ir.attachment'].search([('url','ilike','.css')]).unlink()
self.env['ir.attachment'].search([('url','ilike','.js')]).unlink()
```
3. Guardamos y salimos
```bash
self.env.cr.commit()
exit()
```