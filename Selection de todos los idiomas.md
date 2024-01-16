> [[Back]]

Tags: 
Status: 
Related: 

___

# Selection de todos los idiomas

> [`res_partner.py`](https://github.com/puntsistemes/coralim_odoo/commit/50d863b72540338c6de50c7bda319743d89add56)

```python
def _lang_get(self):
    languages = self.env['res.lang'].with_context(active_test=False).search([]).mapped([])
    return languages.mapped(lambda lang: (lang.code, lang.name))


class ResPartner(models.Model):
    _inherit = "res.partner"

    pnt_documentation_lang = fields.Selection(
        selection=_lang_get,
        string='Documentation language',
    )
```