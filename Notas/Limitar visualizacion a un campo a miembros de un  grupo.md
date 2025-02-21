> [[Configuraciones de permisos]]

Tags: 
Status: 
Related: 

___

# Limitar visualizacion a un campo a miembros de un  grupo

## Heredar un campo en la vista de Odoo 17 y aplicarle `invisible` según el grupo de usuario

En Odoo 17, si queremos heredar un campo en una vista y hacer que sea invisible para los usuarios que no pertenecen a un grupo específico (por ejemplo, "Administrador de Asistencias"), podemos usar la herencia de vistas XML y la propiedad `invisible` junto con `groups`.

### Pasos para lograrlo:

1. **Heredar la vista en un módulo personalizado**.
2. **Aplicar la propiedad `invisible` con una condición de grupos**.

### Ejemplo de código:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<odoo>
    <record id="view_hr_attendance_form_inherit" model="ir.ui.view">
        <field name="name">hr.attendance.form.inherit</field>
        <field name="model">hr.attendance</field>
        <field name="inherit_id" ref="hr_attendance.view_hr_attendance_form"/>
        <field name="arch" type="xml">
            <xpath expr="//field[@name='campo_a_ocultar']" position="attributes">
                <attribute name="invisible">1</attribute>
                <attribute name="groups">your_module.group_attendance_admin</attribute>
            </xpath>
        </field>
    </record>
</odoo>
```

### Explicación del código:

- `inherit_id`: Se referencia la vista original del modelo `hr.attendance`.
- `xpath`: Se localiza el campo que queremos modificar (reemplazar `campo_a_ocultar` por el nombre real del campo).
- `invisible`: Se asigna `1` para ocultar el campo.
- `groups`: Se especifica el grupo `your_module.group_attendance_admin`, lo que hará que solo los usuarios de este grupo puedan ver el campo.

### Creación del grupo de seguridad (si aún no existe)
Si el grupo no está definido, se debe agregar en el archivo de seguridad:

```xml
<record id="group_attendance_admin" model="res.groups">
    <field name="name">Administrador de Asistencias</field>
    <field name="category_id" ref="base.module_category_hr"/>
</record>
```

### Consideraciones:
- Asegúrate de que el ID del grupo (`your_module.group_attendance_admin`) sea el correcto.
- Es recomendable actualizar el módulo después de realizar estos cambios con el comando:
  ```bash
  odoo -u your_module --stop-after-init
  
