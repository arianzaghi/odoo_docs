
> [[Horas]]

Tags: #todo 
Status: 
Related: 

___

# Convertir hora usuario en UTC

```python
from datetime import datetime, timedelta, timezone, utc

now = datetime.now()  
today_at_specified_hour = datetime.combine(  
    now.date(), datetime.min.time()  
) + timedelta(hours=self.pnt_hour_to_trigger)  
  
# Obtener zona horaria del usuario  
user_tz = self.env.user.tz or 'UTC'  # Por defecto UTC si no tiene zona horaria  
user_timezone = timezone(user_tz)  
  
# Convertir la fecha del usuario a UTC  
local_date = user_timezone.localize(today_at_specified_hour)  
utc_date = local_date.astimezone(utc)
```


> En este metodo, quiero establecer 8am y 11pm, pero cuando escribo en bbdd me sale luego 9 y 12.
> Hay que `user_timezone.localize(local_end).astimezone(UTC)`
```python
@api.model  
def default_get(self, fields_list):  
    res = super(RoomBooking, self).default_get(fields_list)  
  
    origin_crm_lead_id = self.env.context.get("pnt_lead_id")  
    if origin_crm_lead_id:  
        lead = self.env["crm.lead"].browse(origin_crm_lead_id)  
  
        res["name"] = f"{lead.pnt_code_sequence} - {lead.name}"  
        user_tz = self.env.user.tz or "UTC"  
        user_timezone = timezone(user_tz)  
  
        if lead.pnt_event_prefered_date_start:  
            # Establecer la hora local en 08:00:00  
            local_start = datetime.combine(lead.pnt_event_prefered_date_start, time(8, 0, 0))  
            # Localizar la fecha en la zona horaria del usuario y convertirla a UTC  
            localized_start = user_timezone.localize(local_start).astimezone(UTC)  
            # Guardar en UTC sin eliminar la información de la zona horaria  
            res["start_datetime"] = localized_start.replace(tzinfo=None)  
  
        if lead.pnt_event_prefered_date_end:  
            local_end = datetime.combine(lead.pnt_event_prefered_date_end, time(23, 56, 59))  
            localized_end = user_timezone.localize(local_end).astimezone(UTC)  
            res["stop_datetime"] = localized_end.replace(tzinfo=None)  
  
    return res
```