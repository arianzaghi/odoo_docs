
> [[040 - Python framework]]

Tags: 
Status: 
Related: 

___

# Coger valor de un campo despues de haberlo cambiado

```python
@api.onchange('pnt_blocked_price')  
def _onchange_category_id(self):  
    if not self.env.user.has_group('custom_pcv.pnt_group_block_sale_price'):  
        original_value = self._origin.pnt_blocked_price  
        self.category_id = original_value  
        return {  
            'warning': {  
                'title': _('Access Denied'),  
                'message': _('Only members of "Block Sale Price" group can modify this field.'),  
            }  
        }
```