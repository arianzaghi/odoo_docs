> [[040 - Python framework]]

Tags: 
Status: 
Related: 

___

# Metodo para validar multiples campos al mismo tiempo

> El objetivo es comprobar si todos estos campos están siendo rellenados cuando un `crm.lead` se marca como ganado.

```python
def _check_compulsory_date_fields_filled(self):  
    compulsory_fields = [  
        "pnt_event_start_date",  
        "pnt_event_end_date",  
        "pnt_assembly_start_date",  
        "pnt_assembly_end_date",  
        "pnt_dissasembly_start_date",  
        "pnt_dissasembly_end_date",  
    ]  
    unfilled_fields = [self._fields[field].string for field in compulsory_fields if not self[field]]  
    if unfilled_fields:  
        raise UserError(  
            _("You must fill all the compulsory date fields to set the lead as won: %s") % "\n ".join(unfilled_fields)  
        )
```

> Se comprueban y después se muestran los `String` de los campos