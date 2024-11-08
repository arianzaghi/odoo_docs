> [[Herencias comunes]]

Tags: 
Status: 
Related: 

___

# Heredar de clase javascript http.controller

> Queremos heredar de la siguiente clase
![[Pasted image 20240902171029.png]]

**Solucion**
```python
from odoo.addons.hr_attendance.controllers.main import HrAttendance  
  
  
class HrAttendance(HrAttendance):  
    def systray_attendance(self, latitude=False, longitude=False):  
        res = super().systray_attendance(latitude=False, longitude=False)  
        return res
```