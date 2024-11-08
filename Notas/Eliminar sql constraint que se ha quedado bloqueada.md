> [[Errores]]

Tags: 
Status: 
Related: 

___

# Eliminar sql constraint que se ha quedado bloqueada

> Hemos creado en un modelo un sql_constraint, pero al eliminarlo no se ha borrado correctamente y nos salta error de validación.
> ![[Pasted image 20241023095410.png]]

```sql
_sql_constraints = [  
    (  
        'unique_pnt_is_unpaid_leave',  
        'unique(pnt_is_unpaid_leave)',  
        _('There can only be one record with "Is unpaid leave" checked.')  
    ),  
    (  
        'unique_pnt_is_paid_leave',  
        'unique(pnt_is_paid_leave)',  
        _('There can only be one record with "Is paid leave" checked.')  
    ),  
    (  
        'unique_pnt_is_unpaid_sickness',  
        'unique(pnt_is_unpaid_sickness)',  
        _('There can only be one record with "Is unpaid sickness leave" checked.')  
    ),  
    (  
        'unique_pnt_is_paid_sickness',  
        'unique(pnt_is_paid_sickness)',  
        _('There can only be one record with "Is paid sickness leave" checked.')  
    ),  
    (  
        'unique_pnt_is_free_disposal_day',  
        'unique(pnt_is_free_disposal_day)',  
        _('There can only be one record with "Free disposal days" checked.')  
    ),  
]
```

```sql
alter table hr_leave_type drop constraint hr_leave_type_unique_pnt_is_unpaid_leave;
```
