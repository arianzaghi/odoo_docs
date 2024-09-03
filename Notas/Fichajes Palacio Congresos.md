> [[Palacio de Congresos Asistencias]]

Tags: 
Status: 
Related: 

___

# Fichajes Palacio Congresos

1. **Modelo Asistencias**
	2. Cuando creamos un fichaje, se corta a las 8hrs (segun el horario).
		- El empleado solo puede ver su horario en el fichaje (no ve las horas reales)
		- El admin puede ver las horas reales trabajadas de cada empleado
		- Guarda entrada y salidas reales y ficticias (las del horario)
	1. Al iniciar una entrada, se debe de crear un `registro de calculo` (uno solo por linea) 
		1. Si ya existía, se añade la asistencia al `registro de cálculo`
	2. Al marcar una salida, se debe de guardar las asistencias en el `registro de cálculo`
2. **Modelo de Calculo**
	1. Se relaciona con un empleado ✅
	2. Se relaciona con 1 o más asistencias ✅
	3. Almacena el total de horas de cada tipo ✅
3. **Modelo Slicitudes**
	1. Se pueden crear desde el modelo de calculo
	2. El empleado puede solicitar horas de cualquier dia indicando:
		- Dia
		- Horas