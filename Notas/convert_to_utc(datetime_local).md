> [[Horas]]

Tags: 
Status: 
Related: 

___

# Convert to UTC (datetime_local)
> Cuando guardamos una fecha en bbdd se guarda en la zona horaria UTC por defecto. Al leer la fecha en bbdd, tenemos que convertirla a nuestra zona actual.

Metodo default de odoo para cambiar la zona
```python
fields.Datetime.context_timestamp(self, leave.date_from)
```


```python
def convert_to_utc(self, datetime_local):  
    """  
    Convierte un datetime a UTC teniendo en cuenta la zona horaria del usuario.    
    """
	
	if not datetime_local:  
        return None  
  
    user_tz = self.env.user.tz or "UTC"  
    local_tz = timezone(user_tz)  
    local_aware = local_tz.localize(datetime_local, is_dst=None)  
    
    return local_aware.astimezone(UTC).replace(tzinfo=None)
```