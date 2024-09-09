> [[Palacio de Congresos Asistencias]]

Tags: 
Status: 
Related: 

___

# Fichajes Palacio Congresos

### **1. Modelo Asistencias**
#### **Funcionalidades Principales:**
1. **Gestión de Fichajes:**
    - **Restricciones de Fichaje:**
        - Los fichajes se cortan automáticamente a las 8 horas según el horario establecido.
        - **Visibilidad:**
            - **Empleado:** Solo puede ver su horario (sin ver las horas reales trabajadas).
            - **Administrador:** Puede ver las horas reales trabajadas por cada empleado.
    - **Almacenamiento de Datos:**
        - Guarda tanto las entradas y salidas reales como las ficticias (horario planificado).
2. **Creación de Registros de Cálculo:**
    - **Al Iniciar una Entrada:**
        - Se debe crear un `registro de cálculo` (uno solo por línea). ✅
        - Si ya existía un registro, se añade la asistencia al `registro de cálculo`. ✅
    - **Visualización de Asistencias:**
        - Solo se muestran las asistencias que encajan con el horario real.
3. **Registro de Asistencias:**
    - **Al Marcar una Salida:**
        - Se guardan las asistencias en el `registro de cálculo`. ✅

### **2. Modelo de Cálculo**
1. **Relaciones del Modelo:**
    - **Relación con Empleado:** Cada registro de cálculo se relaciona con un empleado. ✅
    - **Relación con Asistencias:** Puede estar relacionado con una o más asistencias. ✅
2. **Almacenamiento de Horas:**
    - Guarda el total de horas trabajadas de cada tipo. ✅
3. **Gestión de Peticiones:**
    - **Wizard para Envío de Peticiones:** Los usuarios pueden enviar peticiones directamente desde el modelo. ✅

### **3. Modelo Solicitudes**
1. **Creación de Solicitudes:**
    - **Desde el Modelo de Cálculo:** Las solicitudes se pueden crear directamente desde el modelo de cálculo. ✅
2. **Vistas del Menú:**
    - **Vista FORM:**
        - Botones para aprobar y rechazar solicitudes. ✅
    - **Vista TREE:**
        - **Search View:** Permite filtrar por día. ✅
        - **Acciones Rápidas:** Aceptar o rechazar solicitudes directamente desde la vista tree. ✅
3. **Gestión de Solicitudes:**
    - **Solicitud de Horas por Empleado:**
        - Los empleados pueden solicitar horas para cualquier día, indicando el día y las horas requeridas. ✅
    - **Visualización de Solicitudes:**
        - Las peticiones pueden ser vistas desde el modelo de cálculo. ✅
    - **Impacto de las Solicitudes en el Cálculo:**
        - **Peticiones Aprobadas:** Suman horas al cálculo.
        - **Peticiones Canceladas:** Restan horas del cálculo.

### **Funcionalidades Adicionales**
1. **Notificaciones:**
    - Las peticiones enviadas notifican a los administradores.
2. **Chatter:**
    - Implementado en todos los módulos. ✅
    - **Funcionalidad:** Registra mensajes de modificaciones en el chatter.
3. **Grupos de Permisos:**
    - **Primer Aprobador:**
        - Se asigna un aprobador a cada usuario ✅
        - Los aprobadores solo pueden ver las peticiones de las personas que gestionan (no las suyas propias).
        - Tras primera aprobación, se notifica al segundo aprobador
    - **Segundo Aprobador:**
	    - Grupo de permisos para usuarios con mayor nivel de aprobación.

---
