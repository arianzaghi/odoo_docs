> [[Añadir datos a informe]]

Tags: 
Status: 
Related: [[sale.order]]

___

# Distribución analítica

> La distribución analítica es un campo del modelo `analytic.mixin`, y todas las clases que la usan heredan de este modelo (Sale Order).
```python
class AnalyticMixin(models.AbstractModel):
    _name = 'analytic.mixin'
	_description = 'Analytic Mixin'
    analytic_distribution = fields.Json(
		'Analytic Distribution',
		compute="_compute_analytic_distribution", store=True, copy=True, readonly=False,
    )
```

>Necesitamos widget y permisos para mostrarlo.
```xml
<field name="analytic_distribution" widget="analytic_distribution"  
       groups="analytic.group_analytic_accounting"  
       optional="show"  
/>
```

[[Impedir cambios manuales de distribucion analitica]]