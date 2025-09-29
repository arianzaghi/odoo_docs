> [[domain]]

Tags: 
Status: 
Related: 

___

# Campo auxiliar como filtro para domain

- Guardamos en el campo `pnt_driver_ids` todos los drivers disponibles en el modelo y que pertenecen a una agencia en concreto (campo compute)
- Usamos `pnt_driver_id` para seleccionar uno de los drivers ya filtrados


> [!WARNING] AVISO
> El many2many tiene que tener api.depends. Si no hay campo del que depender, lo haremos sobre el many2one. Motivo: El many2one trigerea un onchange al abrir la vista, y esto carga el many2many


> [`stock_picking.py`](https://github.com/puntsistemes/aditivos_odoo/commit/9a2b9d9dda3fa93629090910fb2a17ebf1d2f873)

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

## Ejemplo 2

```python
pnt_analytic_account_id = fields.Many2one(  
	string="Analytic Account",  
	comodel_name="account.analytic.account",  
	required=False,  
)  

pnt_analytic_account_ids = fields.Many2many(  
	string="Analytic Accounts",  
	comodel_name="account.analytic.account",  
	compute="_compute_pnt_analytic_account_ids",  
	store=False,  
)  

@api.depends("pnt_analytic_account_id")  
def _compute_pnt_analytic_account_ids(self):  
	picking_type = self.env["stock.picking.type"].search(  
		[("pnt_is_construction_site_delivery", "=", True)], limit=1  
	)  
	self.pnt_analytic_account_ids = (  
		self.env["stock.picking"]  
		.search([("picking_type_id", "=", picking_type.id)])  
		.pnt_analytic_account_id.ids  
	)
```