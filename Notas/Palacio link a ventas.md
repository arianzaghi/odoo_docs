> [[Palacio de Congresos 17.0]]

Tags: #todo 
Status: 
Related: 

___

# Palacio link a ventas

```python
def _get_sale_orders_in_header(self):  
    # Field origin has a char containing the sale orders names separated by commas  
    for record in self:  
        sale_orders = self.env['sale.order'].search([('name', 'in', record.origin.split(','))])  
        return sale_orders  
  
def action_view_header_sale_orders(self):  
    self.ensure_one()  
    sale_order_ids = self._get_sale_orders_in_header().ids  
    action = {  
        'res_model': 'sale.order',  
        'type': 'ir.actions.act_window',  
    }  
    if len(sale_order_ids) == 1:  
        action.update({  
            'view_mode': 'form',  
            'res_id': sale_order_ids[0],  
        })  
    else:  
        action.update({  
            'name': _('Sources Sale Orders %s', self.name),  
            'domain': [('id', 'in', sale_order_ids)],  
            'view_mode': 'tree,form',  
        })  
    return action
```

```xml
<xpath expr="//div[@name='button_box']" position="inside">  
    <button class="oe_stat_button" name="action_view_header_sale_orders" type="object" icon="fa-dollar"  
            groups='sales_team.group_sale_salesman' invisible="sale_order_count == 0">  
        <div class="o_field_widget o_stat_info">  
            <span class="o_stat_value">  
                <field name="sale_order_count"/>  
            </span>  
            <span class="o_stat_text">Sale</span>  
        </div>  
    </button>  
</xpath>
```