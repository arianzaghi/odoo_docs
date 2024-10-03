> [[hr.attendance]]

Tags: 
Status: 
Related: 

___

# Heredar del boton de asistencia fichaje

> Queremos heredar del método que se ejecuta al clickar en la bolita del fichaje en v17
> ![[Pasted image 20240927210917.png]]


1. Creamos la carpeta `controllers`
![[Pasted image 20240927210858.png]]
2. Importamos la clase en el `__init__.py`
	`from . import hr_attendance`
3. Heredamos del controlador `hr_attendance.py`
```python
from odoo.http import request  
from odoo.addons.hr_attendance.controllers.main import HrAttendance  
from odoo import http, models, fields  
  
  
class PntHrAttendance(HrAttendance):  
  
    @http.route('/hr_attendance/systray_check_in_out', type="json", auth="user")  
    def systray_attendance(self, latitude=False, longitude=False):  
        res = super().systray_attendance(latitude=False, longitude=False)  
		# Nuestro codigo
        return res
```

## Ejemplo

```python
from odoo.http import request  
from odoo.addons.hr_attendance.controllers.main import HrAttendance  
from odoo import http, models, fields  
  
  
class PntHrAttendance(HrAttendance):  
  
    @http.route('/hr_attendance/systray_check_in_out', type="json", auth="user")  
    def systray_attendance(self, latitude=False, longitude=False):  
        res = super().systray_attendance(latitude=False, longitude=False)  
        # TODO 1 REMOVE CODE  
        employee_id = request.env.user.employee_id  
        current_date = fields.Date.today()  
  
        # Find the attendance record just created by the super method  
        last_attendance = request.env['hr.attendance'].search([  
            ('employee_id', '=', employee_id.id),  
        ], order='check_in desc', limit=1)  
  
        if last_attendance:  
            # Check if a record already exists for today and the current employee  
            daily_calc = request.env['pnt.daily.extra.hour.calc'].search([  
                ('pnt_day', '=', current_date),  
                ('pnt_employee_id', '=', employee_id.id)  
            ], limit=1)  
  
            # If no record exists, create a new one  
            if not daily_calc:  
                daily_calc = request.env['pnt.daily.extra.hour.calc'].create({  
                    'pnt_day': current_date,  
                    'pnt_employee_id': employee_id.id,  
                })  
  
            last_attendance.write({  
                'pnt_extra_hour_calc_id': daily_calc.id,  
            })  
  
        return res
  
```