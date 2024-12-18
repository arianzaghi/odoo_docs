> [[032 - Tipos de Vistas]]

Tags: 
Status: 
Related: 

___

# Añadir vista pivot

1. Miramos las otras vistas que haya en ese modelo (calendar, activity, tree...)
2. Debug > Editar Accion
4. Buscamos el nombre de la accion.
5. Buscamos el action que invoca a esa vista
```xml
<record id="hr_leave_action_new_request_view_tree" model="ir.actions.act_window.view">  
	<field name="sequence">2</field>  
	<field name="view_mode">tree</field>  
	<field name="act_window_id" ref="hr_leave_action_new_request"/>  
	<field name="view_id" ref="hr_leave_view_tree_my"/>  
</record>
	```
4. Creamos un nuevo action igual que el de ejemplo


## `custom_pnt/views/hr_leave.xml`
```xml
<record id="pnt_hr_holidays_view_pivot" model="ir.ui.view">  
    <field name="name">hr.holidays.view.pivot</field>  
    <field name="model">hr.leave</field>  
    <field name="arch" type="xml">  
        <pivot string="Time OFF Analysis">  
            <!-- Filtro por Empleado (Filas) -->  
            <field name="employee_id" type="row"/>  
            <!-- Filtro por Tipo de Ausencia (Filas) -->  
            <field name="holiday_status_id" type="row"/>  
            <!-- Filtro por Rango de Fechas (Columnas, usando date_from como base de tiempo) -->  
            <field name="date_from" type="col" interval="month"/>  
            <field name="date_to" type="col" interval="month"/>  
            <!-- Medida por Número de Días (Sumatoria) -->  
            <field name="number_of_days" type="measure" operator="sum"/>  
        </pivot>  
    </field>  
</record>  
  
<record id="hr_leave_action_new_request_view_pivot" model="ir.actions.act_window.view">  
    <field name="sequence">2</field>  
    <field name="view_mode">pivot</field>  
    <field name="act_window_id" ref="hr_holidays.hr_leave_action_new_request"/>  
    <field name="view_id" ref="pnt_hr_holidays_view_pivot"/>  
</record>
```