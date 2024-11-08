> [[<button> Boton]]

Tags: 
Status: 
Related: 

___

# boton que llama a un metodo

> Sirve para poder llamar a un método en python desde un botón xml

BOTON
```xml
<xpath expr="//header" position="inside">  
    <button name="_update_task_clients" string="Change Partner" type="object" class="btn-primary"/>  
</xpath>
```

TARGET
```python
def _update_task_clients(self):  
    for project in self:  
        if project.partner_id:  
            self.task_ids.write({'partner_id': project.partner_id})
```