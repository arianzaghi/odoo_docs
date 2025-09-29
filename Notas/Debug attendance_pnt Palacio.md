> [[Back]]

Tags: 
Status: 
Related: 

___

# Debug attendance_pnt Palacio

1. Calcs sin asistencia ni leave
```python
self.env["pnt.daily.extra.hour.calc"].search([('pnt_attendance_ids', '=', False), ('pnt_day', '<', '01/09/2025'), ('pnt_leave_ids', '=', False)])
> pnt.daily.extra.hour.calc(2, 81539, 81848, 72646, 72311, 72714, 72739, 82128, 72403, 72715, 82129, 81849, 72740, 72312, 81540)
```

2. Registros creados y modificados de forma sospechosa
![[Pasted image 20250923165946.png]]
3. Registro creado por odoo bot pero modificado de alguna manera.
![[Pasted image 20250923171110.png]]4. Otro registro mal creado (ya existia) pero esta vez creado por gracia modificado por hermi
![[Pasted image 20250923171339.png]]
4. Este registro guarda asistencia pero no peticiones, y el duplicado guarda otra asistencia y peticiones,
![[Pasted image 20250923172011.png]]
Y el otro tiene las peticones pero no la asistencia. Tambien modificado por ellas
![[Pasted image 20250923172112.png]]
Otro creado sin peticiones ni asistencias, mal

![[Pasted image 20250924085121.png]]- Luis Miguel

![[Pasted image 20250924085458.png]]