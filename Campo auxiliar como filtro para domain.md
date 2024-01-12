> [[Back]]

Tags: 
Status: 
Related: 

___

# Campo auxiliar como filtro para domain

- Guardamos en el campo `pnt_driver_ids` todos los drivers disponibles en el modelo y que pertenecen a una agencia en concreto (campo compute)
- Usamos `pnt_driver_id` para seleccionar uno de los drivers ya filtrados


```python
pnt_driver_id = fields.Many2one(
	string="Driver",
	comodel_name="pnt.delivery.carrier.driver",
	domain="[('id','in',pnt_driver_ids)]",
)

pnt_driver_ids = fields.Many2many(
	string="Drivers list",
	comodel_name="pnt.delivery.carrier.driver",
	compute="_compute_drivers",
)
```

```python
@api.depends('pnt_agency')
def _compute_drivers(self):
	for picking in self:
		if self.pnt_driver_id not in picking.pnt_agency.pnt_driver_ids:
			self.pnt_driver_id = False
		picking.pnt_driver_ids = picking.pnt_agency.pnt_driver_ids
```

