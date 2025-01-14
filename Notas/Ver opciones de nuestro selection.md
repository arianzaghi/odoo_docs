> [[Back]]

Tags: 
Status: 
Related: 

___

# Ver opciones de nuestro selection

```python
if not status in [x[0] for x in self._fields['pnt_petition_status'].selection]:  
    raise UserError(_("Invalid status."))
```