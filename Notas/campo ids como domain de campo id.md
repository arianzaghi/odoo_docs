> [[Back]]

Tags: 
Status: 
Related: 

___

# campo ids como domain de campo id

```python
class PntCostsSummaryReportWizard(models.TransientModel):  
    _name = "pnt.costs.summary.report.wizard"  
    _description = "Pnt Costs Summary Report Wizard"  
  
    pnt_analytic_account_id = fields.Many2one(  
        string="Analytic Account",  
        help="Only analytic accounts linked to"  
        "construction site delivery picking types are selectable.",  
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