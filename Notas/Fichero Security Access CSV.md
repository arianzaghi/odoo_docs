> [[050 - Security]]

Tags: 
Status: 
Related: 

___
# Fichero Security Access
> `ir.model.access.csv`

![[Pasted image 20241218111011.png]] ^77a09b
## Añadir permisos a un modelo
**Primera Linea**
```
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
```

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


> [!DANGER] Importante
> Añadir security al `manifest.py`
