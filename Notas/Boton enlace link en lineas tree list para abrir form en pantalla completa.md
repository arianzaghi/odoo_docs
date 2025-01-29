> [[Vista List o Tree - Listado]]

Tags: 
Status: 
Related: 

___

# Boton enlace link en lineas tree list para abrir form en pantalla completa

> Queremos poder abrir una vista en pantalla completa desde el tree en el cuerpo de otro modelo

![[Pasted image 20250129130326.png]]

## 1. Creamos la acción en el modelo destino

```python
class PntPetition(models.Model)

def action_open_form(self):  
    """ Opens the form view of the current record in full screen. """  
    return {  
        "type": "ir.actions.act_window",  
        "res_model": "pnt.petition",  
        "view_mode": "form",  
        "res_id": self.id,  
        "target": "current",  # Abre en pantalla completa  
    }
```

## 2. Creamos el botón en la vista tree del modelo origen

```xml
<separator string="Petitions"/>  
<field name="pnt_petition_ids" readonly="False" nolabel="1">  
    <tree>   
        <field name="pnt_hour_start" widget="float_time"/>  
        <field name="pnt_hour_end" widget="float_time"/>  
        <field name="pnt_description"/> 
		
		%% BOTON ACCION %%
        <button name="action_open_form"  
                type="object"  
                string="Open"  
                icon="fa-external-link"/>  
    </tree>  
</field>
```