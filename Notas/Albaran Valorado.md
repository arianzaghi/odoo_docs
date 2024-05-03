> [[Back]]

Tags: 
Status: 
Related: 

___

# Albaran Valorado

[Usisa v17](https://github.com/puntsistemes/usisa_odoo/pull/10)

## Metodo Total Tax
```python
from odoo import models, fields, api, _  
from odoo.tools import formatLang  
from collections import defaultdict  
  
  
class StockPicking(models.Model):  
    _inherit = "stock.picking"  
  
    def _compute_sale_order_line_fields(self):  
        res = super(StockPicking, self)._compute_sale_order_line_fields()  
        return res  
  
    def pnt_tax_totals(self):  
        names = defaultdict(float)  
  
        for move_line in self.move_line_ids:  
            sale_line = move_line.sale_line  
            if sale_line:  
                taxes = sale_line.tax_id  
                for tax in taxes:  
                    names[tax.description] += move_line.sale_price_subtotal * tax.amount / 100  
  
        amounts = {name: formatLang(self.env, amount, currency_obj=self.currency_id) for name, amount in names.items()}  
  
        return {"names": "\n".join(amounts.keys()), "amounts": "\n".join(amounts.values())}
```

![[Pasted image 20240502094251.png]]


## Tabla de tasas

```xml
<template id="pnt_amount_table_document">  
    <table t-if="pnt_valued_picking and o.move_line_ids and o.state=='done'" class="table table-sm mt32">  
        <thead>  
            <tr>  
                <th class="text-end">  
                    <strong>Untaxed Amount</strong>  
                </th>  
                <th colspan="2" class="text-end">  
                    <strong>Taxes</strong>  
                </th>  
                <th class="text-end">
                    <strong>Total</strong>  
                </th>  
            </tr>  
        </thead>  
        <tbody>  
            <tr>  
                <td class="text-end">  
                    <span t-field="o.amount_untaxed" />  
                </td>  
                <t t-set="tax_totals" t-value="o.pnt_tax_totals()"/>  
                <td class="text-end">  
                    <span t-esc="tax_totals['names']" t-options="{'widget': 'text'}"/>  
                </td>  
                <td class="text-end">  
                    <span t-esc="tax_totals['amounts']" t-options="{'widget': 'text'}"/>  
                </td>  
                <td class="text-end">  
                    <span t-field="o.amount_total" />  
                </td>  
            </tr>  
        </tbody>  
    </table>  
</template>
```