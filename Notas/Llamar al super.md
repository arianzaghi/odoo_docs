> [[Back]]

Tags: 
Status: 
Related: 

___

# Llamar al super

```python
def _prepare_vals_on_create_firstname_lastname(self, vals):  
    values = vals.copy()  
    res = super()._prepare_vals_on_create_firstname_lastname(values)
```