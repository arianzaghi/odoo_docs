> [[Horas]]

Tags: 
Status: 
Related: 

___

# Convertir UTC a horario empleado

> como pasar horas del UTC inglés al UTC del empleado. Además en este método se utiliza la fórmula de las horas hábiles del modelo hr.employee y todo se pasa a horario local del empleado:

```python
    @api.depends('pnt_datetime_init', 'pnt_datetime_finish', 'pnt_responsible_id')  
    def _compute_worked_time(self):  
        for record in self:  
            if record.pnt_datetime_init and record.pnt_datetime_finish and record.pnt_responsible_id:  
                employee = self.env['hr.employee'].sudo().search(  
                    [('user_id', '=', record.pnt_responsible_id.id)])  
                # Obtener zona horaria del empleado  
                employee_tz = timezone(employee.tz or 'UTC')  
                # Se separan las horas-minutos-segundos para obtener las diferencias (en este caso no tiene mucho sentido porque se miran horas)  
                init_datetime = record.pnt_datetime_init.replace(  
                    hour=record.pnt_datetime_init.hour,  
                    minute=record.pnt_datetime_init.minute, second=0, )  
                init_datetime = init_datetime.astimezone(pytz.utc)  
                init_datetime = init_datetime.replace(tzinfo=None)  
                finish_datetime = record.pnt_datetime_finish.replace(  
                    hour=record.pnt_datetime_finish.hour,  
                    minute=record.pnt_datetime_finish.minute, second=0, )  
                finish_datetime = finish_datetime.astimezone(pytz.utc)  
                finish_datetime = finish_datetime.replace(tzinfo=None)

                # Calcular horas trabajadas utilizando el calendario del empleado (está definida en el modelo hr.employee)  
                work_data = employee._get_work_days_data_batch(  
                    init_datetime,  
                    finish_datetime,  
                    compute_leaves=True,  
                    calendar=employee.resource_calendar_id  
                )  
                if work_data:  
                    first_key = next(iter(  
                        work_data))  # Obtener la primera (y única) clave del diccionario  
                    record.pnt_worked_time = work_data[first_key].get('hours',  
                                                                      0.0)  # Obtener 'hours' o 0.0 si no está presente  
            else:  
                record.pnt_worked_time = 0.0
           
```