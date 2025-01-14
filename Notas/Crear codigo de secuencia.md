> [[Back]]

Tags: 
Status: 
Related: 

___

# Crear codigo de secuencia

> Queremos crear un código autoincrementado que podamos utilizar para asignar a registros, igual que se hace con los Pedidos de Venta (`PV20240601`).

![[Pasted image 20250114124130.png]]

## Ejemplo 1: [Palacio HU63223 CRM Lead](https://github.com/puntsistemes/palacio-congresos_odoo/pull/99)

### 1. Secuencia XML
> `data/ir_sequence.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo noupdate="1">  
    <record id="pnt_crm_lead_sequence" model="ir.sequence">  
        <field name="name">CRM Lead Sequencce</field>  
        <field name="code">pnt.crm.lead.sequence</field>
        <field name="padding">10</field>
        <field name="company_id" eval="False"/>  
        <field name="pnt_is_crm_lead_sequence" eval="True"/>  
    </record>  
</odoo>
```

### 2. Secuencia Modelo

```python
# License AGPL-3.0 or later (https://www.gnu.org/licenses/agpl.html).  
from odoo import api, fields, models, _  
from odoo.exceptions import ValidationError  
  
  
class IrSequence(models.Model):  
    _inherit = "ir.sequence"  


	# Campo para identificar esta secuencia
    pnt_is_crm_lead_sequence = fields.Boolean(  
        string="Is Correlative Sequence",  
        default=False,  
    )  

	# Solo puede haber 1 cammpo con la secuencia
    @api.constrains("pnt_is_crm_lead_sequence")  
    def _check_pnt_is_crm_lead_sequence_unique(self):  
        if self.pnt_is_crm_lead_sequence:  
            checked_bool = self.search(  
                [  
                    ("id", "!=", self.id),  
                    ("pnt_is_crm_lead_sequence", "=", True),  
                ]  
            )  
            if checked_bool:  
                raise ValidationError(  
                    _(  
                        "There's already one pnt_is_crm_lead_sequence is checked. Reference : %s"  
                    )  
                    % checked_bool[0].name  
                )
```

### 3. Aplicamos la secuencia en el CREATE del registro

```python
class CrmLead(models.Model):  
    _inherit = "crm.lead"

pnt_code_sequence = fields.Char(  
    string="Code Sequence",  
    readonly=True,  
)

@api.model  
def create(self, vals): 
	# Buscamos la secuencia marcada con el check
    correlative_sequence = self.env["ir.sequence"].search(  
        [("pnt_is_crm_lead_sequence", "=", True)]  
    )  
	
	# Si hay secuencia, recuperamos el siguiente ID
    if correlative_sequence:  
        vals["pnt_code_sequence"] = correlative_sequence.next_by_id()  
        
    return super(CrmLead, self).create(vals)

```

## Ejemplo 2: [Salva ITI HU61093 ](https://github.com/puntsistemes/iti_odoo/commit/16f49b09f4a9c122b64fba2f61120986ef5cef92#diff-bb630b94783e1a8d78adc92d817dd073f969b3e96abb8003ea5a25d4355536a0R1)