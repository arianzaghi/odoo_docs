> [[Contextos]]

Tags: 
Status: 
Related: 

___

# default get

> Este metodo es el encargado de coger los valores por defecto de nuestro modelo para asignarselos. Lo podemos utilizar cuando queramos cargar valores por defecto o pasando por contexto

```python
@api.model  
def default_get(self, fields_list):  
    res = super().default_get(fields_list)
	
	# Conseguimos modelo e id origen
    origin_id = self.env.context.get('params',{}).get('id')  
    origin_model = self.env.context.get('params',{}).get('model')

	# Comprobamos si el modelo y registro existen
	if origin_model == 'crm.lead' and origin_id:  
	    res['name'] = self.env['crm.lead'].browse(origin_id).name
    return res
```
^1cd9f9

Los contextos estan en `self.env.context` y en `self.env.context.params`
![[Pasted image 20241212125629.png]]