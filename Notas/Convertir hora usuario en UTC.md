> [[Back]]

Tags: 
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