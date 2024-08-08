> [[Python framework]]

Tags: 
Status: 
Related: 

___

# Campo horario Hora y Minutos

> Necesitamos un campo horario (para representar horas y minutos), y que solo permita introducir horarios en formato 24h

```python
from odoo import fields, models, api, _
from odoo.exceptions import ValidationError


def _check_valid_time_range(time_value):
    hours = int(time_value // 1)
    minutes = int((time_value % 1) * 60)

    if hours < 0 or hours > 23 or minutes < 0 or minutes > 59:
        raise ValidationError("Time must be between 00:00 and 23:59.")


class ResourceCalendar(models.Model):
    _inherit = 'resource.calendar'

    pnt_night_shift_start = fields.Float(
        string="Nighttime Start Time",
    )

    pnt_night_shift_end = fields.Float(
        string="Nighttime End Time",
    )

    @api.constrains('pnt_night_shift_start', 'pnt_night_shift_end')
    def _check_valid_time(self):
        for record in self:
            _check_valid_time_range(record.pnt_night_shift_start)
            _check_valid_time_range(record.pnt_night_shift_end)
 
```

- Creamos el campo tipo `Datetime`
- Lo mostramos en la vista  con `widget='float_time'` para que solo veamos las horas y los minutos
- Creamos un método de validación de horario, que recibe por parámetro el horario a validar
- Creamos método api.depends que apunte a nuestros campos horarios, y llamamos a su validacion