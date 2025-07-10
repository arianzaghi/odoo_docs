> [[Informe SQL Para vista pivot o tree (como sale_report)]]

Tags: 
Status: 
Related: 

___

# Crear una pivot desde python a traves de consultas SQL

```
class SaleReport(models.Model):  
    _name = "sale.report"  
    _description = "Sales Analysis Report"  
    _auto = False  
    _rec_name = 'date'  
    _order = 'date desc'
```

## Consultas SQL

```sql
select calc.pnt_id,  from pnt_daily_extra_hour_calc AS calc where calc.pnt_day < '02/01/2025'
```

Dudas
- Los campos null le ponemos default 0?


Estoy trabajando en un odoo version 17. Tengo un modelo "calc" que almacena datos en campos de tipo float. Quiero crear una vista pivot a partir de una sentencia sql que me coja los datos del modelo "calc" y me represente como filas cada campo compute de sus ausencias, y ponga las columnas en la fecha.

Utilizamos como ejemplo el modelo sale_report del core:

