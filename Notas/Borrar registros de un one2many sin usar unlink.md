> [[One2many]]

Tags: 
Status: 
Related: 

___

# Borrar registros de un one2many sin usar unlink

> Cuando llamamos al unlink de un modelo B desde un write en un modelo A, a veces se pueden producir errores en que no se borran bien los registros antes de ser creados de nuevo.

```python
self.pnt_extra_hour_detail_ids = [(5,0,0)]
```

```python
# 1. Eliminar los registros de pnt.extra.hour.detail asociados a este registro  

# A veces no elimina correctamente
self.env['pnt.extra.hour.detail'].search([('pnt_extra_hour_id', 'in', self.ids)]).unlink()  

# Forma correcta de borrar todos los registros asociados
self.pnt_extra_hour_detail_ids = [(5,0,0)]
```