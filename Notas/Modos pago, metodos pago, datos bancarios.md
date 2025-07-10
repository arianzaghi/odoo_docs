> [[Añadir datos a informe]]

Tags: 
Status: 
Related: 

___

# Modos pago, metodos pago, datos bancarios

```xml
<!-- Añadimos metodos de pago y condiciones de pago -->  
<xpath expr="//div[@name='signature']" position="after">  
    <div name="payment_details" t-if="o.sale_id">  
        <p t-if="o.sale_id.payment_term_id" name="payment_term">  
            <strong>Payment Term:</strong>  
            <span t-field="o.sale_id.payment_term_id.name"/>  
        </p>  
        <p t-if="o.sale_id.payment_mode_id" name="payment_mode">  
            <strong>Payment Mode:</strong>  
            <span t-field="o.sale_id.payment_mode_id.name"/>  
        </p>  
        <div t-if="o.company_id" name="bank_details"  
             style="font-size: 10pt"  
             class="text-justify float-start">  
            <div class="row">  
                <strong t-if="o.company_id.get_bank_info()">ENTITY:</strong>  
                <span t-esc="o.company_id.get_bank_info()"/>  
                <strong t-if="o.company_id.get_bank_iban()">-</strong>  
                <strong t-if="o.company_id.get_bank_iban()" t-translation="off">IBAN:</strong>  
                <span t-esc="o.company_id.get_bank_iban()"/>  
                <strong t-if="o.company_id.get_bank_swift()">-</strong>  
                <strong t-if="o.company_id.get_bank_swift()">SWIFT/CODE:</strong>  
                <span t-esc="o.company_id.get_bank_swift()"/>  
            </div>  
        </div>  
    </div>  
</xpath>
```

**Para mostrar datos bancarios**
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