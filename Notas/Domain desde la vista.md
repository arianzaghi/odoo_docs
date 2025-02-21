> [[domain]]

Tags: 
Status: 
Related: 

___

# Domain desde la vista

> Lo utilizamos en la accion de un modelo. Esto nos sirve en este caso para ocultar registros de otros empleados que no sean el que realiza la búsqueda

```xml
<field name="domain">[('employee_id.user_id','=',uid)]</field>  
```

```xml
<record id="hr_attendance_theoretical_action" model="ir.actions.act_window">  
    <field name="name">Theoretical vs Attended Time Analysis</field>  
    <field name="res_model">hr.attendance.theoretical.time.report</field>  
    <field  
        name="context"  
    >{'search_default_previous_month': 1, 'search_default_current_month': 1, 'search_default_my': 1}</field>  
    <field name="view_mode">pivot,graph</field>  
    <field name="domain">[('employee_id.user_id','=',uid)]</field>  
    <field  
        name="view_ids"  
        eval="[(5, 0, 0), (0, 0, {'view_mode': 'pivot', 'view_id': ref('hr_attendance_theoretical_view_pivot')}), (0, 0, {'view_mode': 'graph', 'view_id': ref('hr_attendance_theoretical_view_graph')})]"  
    />
```