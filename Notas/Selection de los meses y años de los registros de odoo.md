> [[fields.Selection]]

Tags: 
Status: 
Related: 

___

# Selection de los meses y años de los registros de odoo

> Tenemos en odoo una seria de registros en un modelo. Queremos abrir un wizard que nos permita seleccionar entre los meses, años existentes en los registros de los modelos, para no poder elegir un modelo que 

## Selections
```python
pnt_month = fields.Selection(  
    selection=_get_available_months_in_analytic_lines,  
    string='Month Selection',  
    required=True,  
)  
pnt_year = fields.Selection(  
    selection=_get_available_years_in_analytic_lines,  
    string='Year Selection',  
    required=True,  
)
```
## Meses
```python
def _get_available_months_in_analytic_lines(self):  
    """  
    Devuelve la lista de meses disponibles en las líneas analíticas de los empleados seleccionados,
    traducidos al idioma del usuario actual, con la inicial en mayúscula.
	"""    
    user_lang = self.env.user.lang or 'en_US'  
    dates = self.env['account.analytic.line'].search([]).mapped('date')  
    
    # Obtener los nombres localizados de los meses únicos, con la inicial en mayúscula  
    months = list(set(format_date(date, 'MMMM', locale=user_lang).capitalize() for date in dates))  
    
    # Generar la lista de meses localizados en orden  
    localized_months = [format_date(datetime(2000, i, 1), 'MMMM', locale=user_lang).capitalize() for i in  
                        range(1, 13)]  
                        
    # Ordenar los meses en función del orden localizado  
    months.sort(key=lambda m: localized_months.index(m))  
    
    # Crear la lista de selección con claves en inglés y valores localizados  
    selection_data = [  
        (format_date(datetime(2000, localized_months.index(month) + 1, 1), 'MMMM', locale='en_US'), month)  
        for month in months  
    ]  
    return selection_data
```

## Años
```python
def _get_available_years_in_analytic_lines(self):  
    """  
    Devuelve la lista de años disponibles en las líneas analíticas de los empleados seleccionados.
    """
    years = list(set(x.strftime('%Y') for x in self.env['account.analytic.line'].search([]).mapped('date')))  
    years.sort()  
    selection_data = [(year, year) for year in years]  
    return selection_data
```