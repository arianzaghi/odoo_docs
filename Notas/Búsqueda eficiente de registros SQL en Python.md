> [[Back]]

Tags: 
Status: 
Related: 

___

# Búsqueda eficiente de registros SQL en Python

> Esta clase tiene un método que busca en nuestra bbdd de odoo registros que cumplan las siguientes condiciones:

- **model:** Modelo en el que vamos a buscar registros ('sale.order')
- **field_name_to_search:** Campo a comprobar en el modelo en el que buscamos ('pnt_description')
- **domain:** Dominio en el cual vamos a buscar los registros 
- **field_filter_id:** Valor que usamos para comparar con los registros

### `custom_search.py`
```python
from odoo import api, fields, models  
  
  
class PntSearchSQLdMixin(models.AbstractModel):  
    _name = "pnt.search.sql.mixin"  
    _description = "Search analytic account"  
  
    def _get_disctinct_ids_with_field(  
        self, model, field_name_to_search, domain, field_filter_id  
    ):  
        obj = self.env[model]  
        table_name = obj._table  
        query = obj._search(domain)  
        query.add_where(  
            f'"{ table_name}"."{ field_name_to_search}" ? %s', [str(field_filter_id)]  
        )  
        query.order = f'"{ table_name}"' + '."id"'  
        query_string, query_param = query.select('DISTINCT '+f'"{ table_name}".id')  
  
        self._cr.execute(query_string, query_param)  
        return [pol.get("id") for pol in self._cr.dictfetchall()]
```

### Ejemplos de búsquedas
```python
def _pnt_get_project_purchaseorder_ids(self):  
    self.ensure_one()  
    purchase_order_line_ids = self._get_disctinct_ids_with_field(  
        "purchase.order.line",  
        "analytic_distribution",  
        [],  
        self.analytic_account_id.id  
    )  
    return self.env['purchase.order'].browse(x for x in purchase_order_line_ids)
```
