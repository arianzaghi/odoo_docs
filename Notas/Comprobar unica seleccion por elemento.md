> [[fields.Selection]]

Tags: 
Status: 
Related: [[@api.constrains]]

___
# Comprobar única selección por elemento

> Dentro de un campo seleccionable de tipo One2many queremos que solo se pueda elegir 1 de cada tipo

## Forma avanzada (muchos campos)
```python
@api.constrains(  
    "pnt_is_construction_site_delivery",  
    "pnt_is_construction_site_return",  
    "pnt_is_installed_on_construction_site",  
    "pnt_is_not_installed_on_construction_site",  
    "pnt_is_internal_transfer",  
)  
def _check_pnt_is_construction_site_type(self):  
    field_mappings = {  
        "pnt_is_construction_site_delivery": "construction site delivery",  
        "pnt_is_construction_site_return": "construction site return",  
        "pnt_is_installed_on_construction_site": "installed on construction site",  
        "pnt_is_not_installed_on_construction_site": "not installed on construction site",  
        "pnt_is_internal_transfer": "internal transfer",  
    }  
  
    for field_name, field_description in field_mappings.items():  
        if getattr(self, field_name):  
            existing_record = self.search(  
                [  
                    ("id", "!=", self.id),  
                    (field_name, "=", True),  
                ],  
                limit=1,  
            )  
  
            if existing_record:  
                raise ValidationError(  
                    _(  
                        "There's already one operation type configured as"  
                        " %(field_description)s. Reference: %(reference)s"
					)  
                    % {  
                        "field_description": field_description,  
                        "reference": existing_record.name,  
                    }  
                )
```
## Forma sencilla
### Método `_check_unique_element`
```python
@api.constrains('{{FIELD}}')  
    def _check_unique_{{FIELD}}(self):  
        for record in self:  
            existing_registry = self.search([  
                ('{{FIELD}}', '=', record.{{FIELD}}.id),
                ('id', '!=', record.id)  
            ])  
            if existing_registry:  
                raise ValidationError("{{Error msg}}.")
```

Tenemos un campo de tipo one2Many que permite asignar a cada compañía un sector de producto (alimenticio, industrial....) y asignar a ese sector un dato, en este caso, el número de registro.

Nuestro método comprueba que no pueda existir un sector de producto registrado más de 1 vez en una misma compañía, para asegurar que dentro de esa compañía cada sector tiene su propio número de registro.


```python
from odoo import models, fields, api  
from odoo.exceptions import ValidationError  
  
  
class PntSanitaryRegistry(models.Model):  
    _name = "pnt.sanitary.registry"  
    _description = "Sanitary registry for companies"  
    _rec_name = "pnt_product_sector_id"  
  
    pnt_product_sector_id = fields.Many2one(  
        string="Product's sector",  
        comodel_name="res.partner.industry",  
        required = True,  
    )  
  
    pnt_registry_number = fields.Char(  
        string="Number of sanitary registry",  
        required=True,  
    )  
  
    pnt_company_id = fields.Many2one(  
        "res.company",  
        string="Company owner of the sanitary registry",  
        required=True,  
        default=lambda self: self.env.company,  
    )  
  
    @api.constrains('pnt_product_sector_id', 'pnt_company_id')  
    def _check_unique_product_sector_per_company(self):  
        for record in self:  
            existing_registry = self.search([  
                ('pnt_product_sector_id', '=', record.pnt_product_sector_id.id),  
                ('pnt_company_id', '=', record.pnt_company_id.id),  
                ('id', '!=', record.id)  
            ])  
            if existing_registry:  
                raise ValidationError("This product sector already has a registry for the selected company.")
```