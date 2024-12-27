> [[Back]]

Tags: 
Status: 
Related: 

___

# Archivar un registro

> Este metodo de models es el encargado de archivar registros en otros modelos. Para realizar una accion antes del archivado, heredamos `toggle_active`
## core/odoo/models.py
```python
def action_archive(self):  
	""" Set (x_)active=False on a recordset, by calling toggle_active to  
		take the corresponding actions according to the model  
	"""  
	return self.filtered(lambda record: record[self._active_name]).toggle_active()
```