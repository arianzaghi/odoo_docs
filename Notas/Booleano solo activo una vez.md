> [[040 - Python framework]]

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

## Para dos booleanos
```python
@api.onchange('pnt_is_first_approval_activity', 'pnt_is_second_approval_activity')  
def _check_pnt_portal_particular_default(self):  
    if self.pnt_is_first_approval_activity and self.pnt_is_second_approval_activity:  
        raise ValidationError(_("An activity can't be both first and second approval."))  
  
    if self.pnt_is_first_approval_activity:  
        checked_first = self.search(  
            [("id", "!=", self.id), ("pnt_is_first_approval_activity", "=", True)]  
        )  
        if checked_first:  
            raise ValidationError(  
                _("There's already one activity for first approvals. Reference: %s") % checked_first[0].name  
            )  
  
    if self.pnt_is_second_approval_activity:  
        checked_second = self.search(  
            [("id", "!=", self.id), ("pnt_is_second_approval_activity", "=", True)]  
        )  
        if checked_second:  
            raise ValidationError(  
                _("There's already one activity for second approvals. Reference: %s") % checked_second[0].name  
            )
```

Palacio Congresos v17 => HU53587 Informe Agregado I => mail_activity_tpe.py