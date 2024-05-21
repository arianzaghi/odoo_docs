> [[Odoo Modelos|Back]]

Tags: #modelo 
Status: 
Related: [[account.move.line]]

___

# account.move

> Facturas

> Contabilidad > Clientes > Facturas


## Utils

### formatLang()

```python
def formatLang(env, value, digits=None, grouping=True, monetary=False, dp=False, currency_obj=False):
```

```python
res.append({  
    'product_name': lot.product_id.display_name,  
    'quantity': formatLang(self.env, invoiced_lot_qty, dp='Product Unit of Measure'),  
    'uom_name': lot.product_uom_id.name,  
    'lot_name': lot.name,  
    # The lot id is needed by localizations to inherit the method and add custom fields on the invoice's report.  
    'lot_id': lot.id,  
})
```

