> [[Back]]

Tags: 
Status: 
Related: 

___

# Check Bool Unico por elemento muchos campos

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