
> [[Añadir datos a informe]]

Tags: 
Status: 
Related: [[Pedido de Venta (PV)]]

___

# Mostrar datos bancarios de la compañía

> Queremos mostrar los datos bancarios de nuestra compañía en un informe 

```python
from odoo import fields, models, api  
  
  
class ResCompany(models.Model):  
    _inherit = 'res.company'  
  
    def get_bank_info(self):  
        self.ensure_one()  
        banks = self.partner_id.bank_ids  
        return banks[0].bank_name if banks else ""  
  
    def get_bank_iban(self):  
        self.ensure_one()  
        banks = self.partner_id.bank_ids  
        return banks[0].acc_number if banks else ""  
  
    def get_bank_swift(self):  
        self.ensure_one()  
        banks = self.partner_id.bank_ids  
        return banks[0].bank_bic if banks else ""
```

```xml
<xpath expr="//div[p[@id='fiscal_position_remark']]" position="after">  
	<div name="first_row"  
		 style="font-size: 10pt"  
		 class="text-justify float-start">  
		<div>  
			OUR BANK DATA FOR TRANSFER PAYMENT  
		</div>  
		<div class="row">  
			<div class="col-12">  
				<strong>ENTITY:</strong>  
				<span t-esc="doc.company_id.get_bank_info()"/>  
				<strong t-translation="off">IBAN:</strong>  
				<span t-esc="doc.company_id.get_bank_iban()"/>  
				<strong>-</strong>  
				<strong>SWIFT/CODE:</strong>  
				<span t-esc="doc.company_id.get_bank_swift()"/>  
			</div>  
		</div>  
	</div>  
</xpath>  
```