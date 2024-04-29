> [[Back]]

Tags: 
Status: 
Related: 

___

# Modelo mantenimiento con TREE

[Bonagent v15]()


```python
from odoo import models, fields  
  
  
class PntResPartnerJob(models.Model):  
    _name = "pnt.res.partner.job"  
    _description = "Jobs"  
    _rec_name = "pnt_name"  
  
    pnt_name = fields.Char(string="name")  
    pnt_description = fields.Text(string="Description", required=False)
```

```python
from odoo import models, fields  
  
class PntResPartnerJobRelation(models.Model):  
    _name = "pnt.res.partner.job.relation"  
    _description = "Res Partner Job Relation"  
    _rec_name = "pnt_observation"  
  
    pnt_observation = fields.Text(string="Observation")  
    pnt_partner_id = fields.Many2one(string="Jobs", comodel_name="res.partner")  
    pnt_job_id = fields.Many2one(string="Jobs", comodel_name="pnt.res.partner.job")
```