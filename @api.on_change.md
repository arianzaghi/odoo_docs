> [[Back]]


Tags: #decorador
Status: 
Related: 

___

# @api.onchange

El decorador "@api.onchange" se usa para definir métodos que se activan automáticamente cuando se modifican campos específicos.

Se utiliza comunmente para actualizar o recalcular dinámicamente campos relacionados en respuesta a las interacciones del usuario.

Cuando se modifica un campo incluido en el decorador, se invoca el método asociado, lo que permite a los desarrolladores implementar lógica personalizada para actualizar otros campos según los cambios.

**Example**
```python
@api.onchange('driver_id')
def onchange_field_name(self):
    self.driver_name = False
```
