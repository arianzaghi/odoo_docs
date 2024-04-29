> [[Back]]

Tags: 
Status: 
Related: 

___

# Security

> `ir.model.access.csv`

## Añadir permisos a un modelo

**Copy-Paste**
```python
{{MODULO}}.access_{{MODELO}},access_{{MODELO}},{{MODULO}}.model_{{MODELO}},base.group_user,1,1,1,1
```
- Reemplazamos `{{MODULO}}` por `module_name` (`custom_pnt`)
- Reemplazamos `{{MODELO}}` por `model_name` (`pnt_test_class`)

**Ejemplo**
```python
report_pnt.access_out_picking_label_wizard,access_out_picking_label_wizard,report_pnt.model_out_picking_label_wizard,base.group_user,1,1,1,1
```
