> [[070 - Testing]]

Tags: 
Status: 
Related: 

___

# Ejemplo Tests

> `-c /opt/sources/odoo170/conf/palacio.conf -d crmPrueba -i crm_pnt --test-tags pnt`

## `palacio/crm_pnt/tests/common.py`
```python
from odoo.tests import TransactionCase, tagged  
  
@tagged('pnt')  
class TestCrmPnt(TransactionCase):  
    def setUp(self):  
        super(TestCrmPnt, self).setUp()  
        self.partner = self.env['res.partner'].create({  
            'name': 'Test Partner'})  
  
    def pnt_init_sequence(self, xmlid):  
        sequence = self.env.ref(xmlid)  
        sequence.number_next_actual = 1  # Reset the sequence
```

## `palacio/crm_pnt/tests/test_crm_lead.py`
```python
from .common import TestCrmPnt  
  
class TestCrmLead(TestCrmPnt):  
  
    def test_create(self):  
        # Reset the sequence  
        self.pnt_init_sequence('crm_pnt.pnt_crm_lead_sequence')  
        # Create a new lead  
        lead = self.env['crm.lead'].create({  
            'name': 'Test Lead 1',  
            'partner_id': self.partner.id})  
            
        # Check that the lead was created with a sequence  
        self.assertEqual(lead.pnt_code_sequence, '0000000001')  
        
        lead = self.env['crm.lead'].create({  
            'name': 'Test Lead 2',  
            'partner_id': self.partner.id})  
            
        # Check that the lead was created with a sequence  
        self.assertEqual(lead.pnt_code_sequence, '0000000002')
```