> [[fields.Selection|Back]]

Tags: 
Status: 
Related: [[fields.Selection]]

___

# Selection de idiomas activos

> [`res_partner.py`](https://github.com/puntsistemes/coralim_odoo/commit/50d863b72540338c6de50c7bda319743d89add56)

```python
def _lang_get(self):
    return self.env['res.lang'].get_installed()


class ResPartner(models.Model):
    _inherit = "res.partner"

    pnt_documentation_lang = fields.Selection(
        selection=_lang_get,
        string='Documentation language',
    )
```

