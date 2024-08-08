> [[Modulos custom de punt]]

Tags: 
Status: 
Related: 

___

# Palacio de Congresos

## 1. Tabla con horarios de nocturnidad ✅
> Modelo mantenimiento que registra el inicio y fin del horario nocturno.

> [!WARNING] Historia duplicada
> **[HU53578]: Horas Nocturnidad** -> Hemos añadido esto mismo dentro de una pestaña en el horario de trabajo
> Debemos de moverlo a un modelo nuevo.

**Mantenimiento `night shift`**
- Nombre del tramo nocturno
- Fecha inicio tramo nocturno
- Fecha fin tramo nocturno
- Hora inicio tramo nocturno
- Hora fin tramo nocturno

**Requisitos**
- Poder cambiar mediante un desplegable en `ajustes` el tramo de `night shift` que vamos a ver
- Poder crear nuevo tramo (Poner fecha fin previo tramo = fecha inicio tramo actual)
- Ponderaciones editables por el admin

## 2. Tabla con ponderaciones de horas extra ✅

> Modelo mantenimiento que registra para un periodo de tiempo, las ponderaciones de los tipos de horas

![[Pasted image 20240731143012.png]]

![[Pasted image 20240725095544.png]]

### **Modelo mantenimiento `extra_hours_coefficient`**
- Nombre del tramo
- Fecha inicio tramo
- Fecha fin tramo
- Valores de ponderación
	- Hora extra 1.25
	- Hora festivo 1.5
	- Hora nocturno 1.25

### **Requisitos**
- Poder cambiar mediante un desplegable en `ajustes` el tramo de ponderaciones que queremos visualizar.
	- Por defecto se muestra el tramo activo
	- Desde ajustes no podemos modificar los tramos
- Poder crear/editar nuevo tramo de ponderaciones desde `asistencia>configuracion>ponderaciones`
- Solo permitido crear/editar al administrador

### Restricciones
- Nuevos tramos deben ser consecutivos con los existentes
- Las ponderaciones deben de ser ">1" en todos los casos
- Solo puede haber un tramo activo a la vez

## 3. Horas teóricas de calendario ✅
> Cálculo del total de horas teóricas trabajables en un año en base a un calendario determinado.

Para realizar el cálculo de horas trabajables en un año dentro de un calendario teniendo en cuenta los dias festivos:
- Calculamos el número de horas de trabajo por día de la semana
- Calculamos el total de horas trabajables en el año en curso (1/1 hasta 31/12)
- Finalmente, por cada día festivo, descontamos del total las horas que se deberían haber trabajado según el día de la semana en que cae


## 4. Calendarios  🚧🔨⏳
> Asignación de calendarios festivos y cálculo de horas trabajables

1. Calendario Normal de los trabajadores
	1. Lo usaremos para calcular las horas teóricas trabajables del empleado (contando festivos)
	2. Pueden haber varios calendarios según las necesidades
	3. Deben de incluir `límite_máximo_horas_trabajables` (STANDBY)
2. Calendario Fines de Semana
	1. Muestran los horarios de trabajo dentro de los fines de semana
		- Esto lo necesitamos para poder saber si en un fin de semana han habido: horas extra, 
	2. Se diferencian del resto mediante un booleano.
	3. Cada empleado debe tener su calendario normal y calendario fin de semana asignados.
	4. Hay un calendario de fin de semana por cada calendario normal.

## 5. Fichajes (STANDBY) 
> Queremos mantener información de:
> - Fichaje de horas real
> - Fichaje de horas sin contar las que se pasan del límite

**Requisitos**
1. Al Marcar la salida, se deben actualizar las horas de **salida del fichaje**:
	- Fichaje salida del core
		- Si se han trabajado más horas del límite --> `fichaje_inicio` + `limite de horas`
		- Si no se ha superado el límite --> `fichaje salida core` = `fichaje salida real`
	- Fichaje de salida real
		- Marca la hora de salida REAL del usuario.
		- Puede ser igual, inferior o superior al límite.
3. La diferencia de horas (aquellas horas trabajadas por encima del `límite_máximo_horas_trabajables`) se deben guardar como `horas_extra`
4. Las `horas extra` se deben de poder enviar para aprobación `enviar_solicitud_horas_extra`
	- Las `horas extra` deben de guardarse (acumuladas) dentro del día del fichaje.
	- Cuando se aprueban las `horas extra`, se calculan los coeficientes y se suman las ausencias.


> [!DANGER] Fichajes irregulares NO nocturnos
> **Problema 1:** a la hora de calcular las horas extra cuando:
> 8h max, MARTES
> 4am --> 8am --> (4hrs)
> 8am --> 14am--> (8hrs)
> - Inicio de la jornada en el mismo día
> - Jornada superior al máximo
> - Las horas fuera del horario (4am a 8am) deberian ser solo extra, no nocturnas
> 
> **Problema 2:** Entramos a trabajar 5 minutos antes
> 8h max, MARTES
> 7:55 --> 16:55
> - Estableciendo 8 horas máximas y horarios: Tenemos 5 minutos de horas extra.
> - Estos 5 minutos NO deberían contar como *nocturnas*, solo como *extra*

> [!Info] Fichaje en un dia y salida en otro
> 
> **Planteamiento:**
> ¿Que ocurre cuando un empleado tiene fichaje de entrada en un día y fichaje de salida en otro día diferente?
> 
> **Ejemplo**:
> - Fichaje de entrada 25/07/2024 - 20:00
> - Fichaje salida 26/07/2024 - 4:00
> - Fichaje de entrada 26/07/2024 - 14:00
> - Fichaje de salida 26/07/2024 - 22:00
> 
> Tenemos un fichaje de 8h  y otro fichaje de 8h.
> El 25/07/2024 tenemos 4h trabajadas
> El 26/07/2024 tenemos 12h trabajadas
> 
> ¿Debemos de considerar 4h como horas extra?
> 
> **Respuesta:**
> Esos dos fichajes de 8h cada uno con periodo de descanso entre ellos deben ser computados como dos jornadas de trabajo independientes, aunque algunas horas de ambos turnos coincidan en el mismo día natural. 
> 
> Por tanto, esas 4h de exceso no deben ser computadas como extras, porque ha habido un periodo de descanso entre ambos turnos de trabajo.
> 

## 6. Informes / Visualización de datos

