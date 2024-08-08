> [[Chatter]]

Tags: 
Status: 
Related: 

___

# Mostrar mensaje en chatter después de un evento

## Tracking simple

> Usamos el valor `tracking` para determinar si se van a registrar los cambios en el chatter
```python
name = fields.Char(required=True, tracking=True)
```
> También podemos indicar niveles de tracking. Los niveles de seguimiento pueden variar de 0 a 3, donde 0 significa sin seguimiento y 3 es el nivel más alto de seguimiento.
```python
name = fields.Char(required=True, tracking=3)
```

## Tracking avanzado
[Signes](https://github.com/puntsistemes/ajsignes_odoo/pull/19)
[Coralim](https://github.com/puntsistemes/coralim_odoo/commit/fabb972a7251d12ca21a704a4914ce97e0fb8796)