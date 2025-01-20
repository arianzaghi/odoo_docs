> [[040 - Python framework]]

Tags: 
Status: 
Related: 

___

# Archivar un registro

> Este metodo de models es el encargado de archivar registros en otros modelos. Para realizar una action antes del archivado, heredamos `toggle_active`.

> `action_archive` recorre self y por cada registro, llama a `toggle_active`
## `action archive` core/odoo/models.py
```python
def action_archive(self):  
	""" Set (x_)active=False on a recordset, by calling toggle_active to  
		take the corresponding actions according to the model  
	"""  
	return self.filtered(lambda record: record[self._active_name]).toggle_active()
```

## `toggle active` src/core/odoo
```python
def toggle_active(self):  
    "Inverses the value of :attr:`active` on the records in ``self``."  
    active_recs = self.filtered(self._active_name)  
    active_recs[self._active_name] = False  
    (self - active_recs)[self._active_name] = True
```

# Archivar registros relacionados cuando se archiva el padre

> Tenemos un modelo `A` que esta relacionado mediante `many2one` con B y C. Queremos que al archivar `A`, se archiven `B`
 y `C`.
 
```python
def toggle_active(self):  
    """  
	Override the toggle_active method to synchronize the active state
	of related project and analytic account when a lead is archived    or unarchived.
	""" 
	
	super(CrmLead, self).toggle_active()  
	
	if self.{{FIELD_A}}:  
		self.{{FIELD_A}}.sudo().write({'active': self.active})  
	if self.{{FIELD_B}}:  
		self.{{FIEFIELD_BLD_A}}.sudo().write({'active': self.active})
```