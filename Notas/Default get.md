> [[Contextos]]

Tags: 
Status: 
Related: 

___

# default get

> Este método es el encargado de coger los valores por defecto de nuestro modelo para asignarselos. Lo podemos utilizar cuando queramos cargar valores por defecto o pasando por contexto

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


> [!DANGER] Cuidado!!
> A veces el `params` del `context` falla y viene vacío cuando antes había venido lleno.
> Para solucionarlo:

```xml
    <separator string="Room Bookings"/>  
    # PASAMO POR CONTEXTO EL ID DEL MODELO DESDE EL QUE SE CREA EL REGISTRO DEL MODLEO 2
    <field name="pnt_room_booking_ids" mode="tree,gantt" context="{'pnt_lead_id': id}">  
        <tree string="Rooms" editable="bottom">  
            <field name="name"/>  
            <field name="pnt_is_blocked" optional="hide"/>  
            <field name="pnt_is_unlocked" readonly="not pnt_is_blocked"/>  
            <field name="start_datetime"/>  
            <field name="stop_datetime"/>  
            <field name="room_id" domain="[('pnt_is_event_available', '=', True)]"/>  
            <field name="organizer_id"/>  
        </tree>  
    </field>  
```



