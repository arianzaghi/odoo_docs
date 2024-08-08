> [[Back]]

Tags: 
Status: 
Related: 

___

# varios many2many en un solo modelo

> Cuando tenemos varios many2many apuntando a un solo modelo, odoo se puede confundir y utilizar la tabla generada por la relacion que no toca. Para evitar esto:


```python
pnt_domain_picking_ids = fields.Many2many(  
    string='Nombre del campo',  
    comodel_name='stock.picking', # Modelo con el que se relaciona  
    relation="pnt_domain_picking_move_ids",  # Campo que usa para la relacion
    column1="move_id",  # Modelo actual
    column2="picking_id",  # Modelo destino
)
```