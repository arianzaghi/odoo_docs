> [[Python framework]]

Tags: 
Status: 
Related: [[@api.constrains]]

___

# Booleano solo activo una vez

```python
from odoo.exceptions import ValidationError

@api.constrains("pnt_portal_particular_default")
def _check_pnt_portal_particular_default(self):
    if self.pnt_portal_particular_default:
        checked_bool = self.search(
            [("id", "!=", self.id), ("pnt_portal_particular_default", "=", True)]
        )
        if checked_bool:
            raise ValidationError(
                _(
                    "There's already one pnt_portal_particular_default is checked. Reference : %s"
                )
                % checked_bool[0].name
            )
```