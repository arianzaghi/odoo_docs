> [[Utils]]

Tags: 
Status: 
Related: 

___

# Convertir fecha en UTC a zona horaria del usuario

> Cuando guardamos una fecha en bbdd se guarda en la zona horaria UTC por defecto. Al leer la fecha en bbdd, tenemos que convertirla a nuestra zona actual.

```python
fields.Datetime.context_timestamp(self, leave.date_from)
```