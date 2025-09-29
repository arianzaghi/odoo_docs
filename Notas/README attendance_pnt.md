# Módulo de Gestión de Horas Extra para Odoo

  

## Descripción General: `attendance_pnt`

  

Este módulo permite a los usuarios gestionar peticiones de horas extra en el trabajo, integrándose con los módulos estándar de asistencia y vacaciones de Odoo. Proporciona un flujo de validación, cálculo y reporte de horas extra, así como herramientas para la administración y seguimiento de las mismas.
## Funcionalidades Principales
- **Gestión de Peticiones de Horas Extra:**
- Las peticiones de horas extra se crean automáticamente a partir de los registros de asistencia en Odoo (cuando se registra entrada y salida).
- Los usuarios no pueden crear peticiones manualmente.
- El sistema determina el estado inicial de la petición (borrador o aceptada) según si la asistencia supera o no el horario permitido para ese día.
- Las peticiones que no sean autovalidadas requieren una descripción personalizada antes de poder ser enviadas y pasar por los estados de aprobación (borrador, pendiente, segunda aprobación, aceptada o rechazada).
- El cálculo de las horas de inicio y fin de cada petición se realiza automáticamente al finalizar el fichaje.

- **Cálculo Automático de Horas Extra:**

- El sistema calcula automáticamente las horas extra trabajadas a partir de las peticiones aceptadas y el calendario laboral del empleado.

- Considera diferentes tipos de horas: normales, festivas, nocturnas y sus combinaciones.

- Bonificaciones automáticas según reglas configurables (Ponderaciones).

  

- **Integración con Asistencias y Vacaciones:**

- Relación directa con los registros de asistencia (`hr.attendance`) y ausencias (`hr.leave`).

- Control de teletrabajo y motivos asociados.

  

- **Reportes y Análisis:**

- Reportes detallados de horas extra por empleado, día y tipo de hora.

- Vistas analíticas para el seguimiento y control de las horas extra y balances.

  

- **Configuración y Seguridad:**

- Reglas de acceso y seguridad para proteger la información sensible.

- Configuración de coeficientes de bonificación y reglas de validación.

  

## Guía para Usuarios

  

### 1. Validación y Seguimiento

  

- Las peticiones pueden requerir una o dos aprobaciones según la configuración.

- El estado de la petición se actualiza automáticamente y se notifican a los usuarios implicados.

- Puedes consultar el historial y estado de tus peticiones desde la vista de formulario.

  

### 2. Cálculo Automático

  

- El sistema puede generar peticiones automáticas basadas en los registros de asistencia.

- Las horas extra se calculan considerando el calendario laboral, ausencias y reglas de la empresa.

  

### 3. Reportes

  

- Accede al menú de reportes para visualizar y exportar informes de horas extra.

- Los reportes incluyen desglose por tipo de hora, empleado y periodo.

  

### 4. Configuración

  

- Los administradores pueden definir reglas de bonificación, tipos de teletrabajo y parámetros de validación desde el menú de configuración.

  

## Créditos

  

- **Autor:** Arian Zaghi - Punt Sistemes ([https://www.puntsistemes.es](https://www.puntsistemes.es))

  

---

  

## Documentación Adicional

  

- **[Modelos](modelos.md)**: Documentación técnica detallada de todos los modelos del módulo

- **[Flujos](flujos.md)**: Explicación completa de los procesos y flujos de trabajo

- **[Configuración](configuracion.md)**: Guía técnica de configuración, permisos y automatización

- **[FAQ](FAQ.md)**: Preguntas frecuentes y soluciones a problemas comunes

  

> Para más detalles sobre cada modelo, flujo o pantalla, consulta los archivos específicos dentro de esta carpeta de documentación.