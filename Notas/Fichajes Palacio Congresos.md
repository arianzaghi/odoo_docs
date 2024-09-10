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
        - También para registros creados MANUALMENTE
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
4. **Tipos de fichajes en un dia:**

| Fichaje | Entrada | Salida | Horas Nocturnas | Contemplado |
| :-----: | ------- | ------ | --------------- | :---------: |
|    1    | 7:00    | 12:00  | 1+0=1           |             |
|    2    | 18:00   | 22:00  | 0+2=2           |      ✅      |
|    3    | 7:00    | 22:00  | 1+2=3           |      ✅      |
|    4    | 12:00   | 18:00  | 0+0=0           |             |
|    5    | 22:00   | 23:00  | 0+1=1           |             |
|    6    | 5:00    | 7:00   | 2+0=2           |      ✅      |
|    7    | 21:00   | 7:00   | 0+10=10         |             |
|    8    | 21:00   | 10:00  | 0+11=11         |             |
|    9    | 18:00   | 7:00   | 0+11=11         |             |
|   10    | 18:00   | 10:00  | 0+10=10         |      ✅      |
|   11    | 22:00   | 21:00  | 2+11=13         |             |

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
        - Los aprobadores solo pueden aprobar las peticiones de las personas que gestionan (no las suyas propias) ✅
        - Tras primera aprobación, se notifica al segundo aprobador
    - **Segundo Aprobador:**
	    - Grupo de permisos para usuarios con mayor nivel de aprobación.

---

> Estamos desarrollando un sistema en odoo para solicitar horas extra mediante peticiones. Las peticiones tienen primera y segunda validacion. Cada empleado tiene asignado a un responsable de validacion de horas. Tras la aprobación de la peticion por el responsable, tenemos que esperar a la aprobacion del administrador. El modelo "calculo" almacena las asistencias de un empleado. Se crea un registro por dia de trabajo del empleado. Desde este modelo podemos crear peticiones de horas libres, que deberan ser aprobadas por nuestro aprobador y después por el administrador. Cuando entramos al modelo calculo podemos ver todos nuestros fichajes en ese dia y crear o acceder al listado de peticiones ya creadas para ese mismo dia (por ejemplo: si hemos trabajado 2 horas extra, creariamos la peticion desde este modelo y se crearia un nuevo registro en el modelo de peticiones). Las restricciones son las siguientes: - Las peticiones unicamente pueden ser vistas por: - El solicitador de la peticion - El aprobador del que solicita la peticion - El administrador, que tiene acceso a todos los registros. - Los registros del modelo calculo solo pueden ser vistos por: - El propio usuario dueño del registro - El administrador