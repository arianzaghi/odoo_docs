> [[Python framework]]

Tags: 
Status: 
Related: 

___

# Campo obligatorio en Pedido de Venta

```python
class SaleOrder(models.Model):  
    _inherit = 'sale.order'  
  
    def action_confirm(self):  
        for order in self:  
            for line in order.order_line:  
                if not line.pnt_billing_date:  
                    raise ValidationError(  
                        _("Field 'Billing Date' must be filled in on all order lines when confirming the sale order.")  
                    )  
                if not line.pnt_accounting_entry_date:  
                    raise ValidationError(  
                        _("Field 'Accounting entry date' must be filled in on all order lines when confirming the sale order.")  
                    )  
                if not line.pnt_sale_tag:  
                    raise ValidationError(  
                        _("Field 'Sale Tag' must be filled in on all order lines when confirming the sale order.")  
                    )  
        return super(SaleOrder, self).action_confirm()
```