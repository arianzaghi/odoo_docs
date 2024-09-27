> [[Palacio de Congresos Asistencias]]

Tags: 
Status: 
Related: 

___

# Fichajes Palacio Congresos

Este documento detalla la funcionalidad de una aplicación en Odoo para la gestión de las asistencias, el registro de horas extra solicitadas por los empleados, y la revisión de dichas solicitudes por parte de los aprobadores. Cada modelo se describe con sus funcionalidades específicas y su implementación.


**TO DO**
- [ ] Eliminar boton create de **Petitions**
- [ ] Traducir codigo al ingles
- [ ] Eliminar magic night schedule
- [ ] Cuando se elimina una peticion, comprobar si es autovalidada para sumar las horas a las restantes
- [ ] Traducir todo a ES
- [ ] No mostrar horas kiosco cuando se crea una peticion manual

\
### **1. Modelo Asistencias**
#### 1. **Permisos:**
- Los usuarios no pueden acceder a sus asistencias
- Los usuarios no pueden modificar sus asistencias
- Los usuarios no pueden crear asistencias
#### 2. **Al Crear asistencias:**
- Se crea un `registro de cálculo` para ese `dia` y `empleado` (si no existía uno). ✅
- Se vincula la asistencia al `registro de cálculo`. ✅

- **Fichaje de odoo:**
	- Se cortan automáticamente a las horas teóricas según el horario establecido. ✅
	- Si el fichaje es inferior a las `horas teóricas`, se deja tal como esta ✅
- **Fichaje Real:**
	- Se mantienen reflejando la realidad ✅
	- No se pueden modificar ✅
	- Si el fichaje es manual, no hay e/s real ⏰
- **Creación automática de peticiones:**
	- Si la asistencia es inferior a las horas teóricas por trabajar en el dia, se crea una peticion autovalidada ✅
	- Si la asistencia es superior a las horas teóricas por trabajar en el dia se crea una peticion autovalidada y una peticion de horas extra pendiente de enviar✅
	- Si al crear la asistencia no quedan horas teóricas por trabajar, no se crea nada automáticamente✅
	- Todas las peticiones creadas automáticamente se relacionan con la asistencia✅
#### 3. **Eliminar asistencias**
- No se puede eliminar una asistencia si tiene una solicitud de horas asociada. ✅
- Si se borra una asistencia, se eliminan también sus calc asociadas si se quedan sin asistencias. ✅
- Evitar que si se modifica una asistencia, se puedan generar solicitudes duplicadas. ✅
- Al eliminar un `registro de cálculo`, debe aparecer un aviso si tiene solicitudes asociadas. ✅

### **2. Modelo de Cálculo**
> Este modelo guarda la información de las horas de trabajo de un empleado durante un día.
> El registro se crea cuando se añade la primera asistencia del día.
> Desde este modelo se gestionan también las peticiones.
1. **Relaciones del Modelo:**
    - **Relación con Empleado:** Cada registro de cálculo se relaciona con un empleado. ✅
    - **Relación con Asistencias:** Puede estar relacionado con una o más asistencias. ✅
    - Guarda el total de horas trabajadas de cada tipo. ✅
2. **Gestión de Peticiones:**
    - **Wizard para Envío de Peticiones:** Los usuarios pueden enviar peticiones directamente desde el modelo. ✅
    - Los usuarios pueden visualizar las peticiones asociadas a ese día ✅
3. **Calculo calculo de horas**
	1. Se pueden enviar todas las peticiones que se quieran para validar✅
	2. Al validar la primera peticion, se hace el calculo de las horas correspondientes y se añade al total ✅
	3. Las siguientes peticiones que se hagan, al ser validadas:
		1. Se eliminan todas las horas calculadas de ese dia ✅
		2. Se ordenan las peticiones cronologicamente ✅
		3. Se procesan todas las peticiones que ya habian sido validadas + la nueva ✅
#### 2. **Eliminar registros**
- No se puede borrar calc si hay asistencias vinculadas ✅
- Se borra el calc si se queda sin asistencias ✅
- Si un calc sin asistencias se borra, se eliminan todas las peticiones 'libres' ✅
### **3. Modelo Peticiones**
#### 1. **Crear  Peticiones:**
- Las solicitudes SOLO se pueden crear desde el modelo de cálculo. ✅
- Botones para aprobar y rechazar solicitudes. ✅
- **Search View:** Permite filtrar por día. ✅
- **Acciones Rápidas:** Aceptar o rechazar solicitudes directamente desde la vista tree. ✅
1. **Gestión de Solicitudes:**
    - **Solicitud de Horas por Empleado:**
        - Los empleados pueden solicitar horas para cualquier día, indicando el día y las horas requeridas. ✅
    - **Visualización de Solicitudes:**
        - Las peticiones pueden ser vistas desde el modelo de cálculo. ✅
    - **Impacto de las Solicitudes en el Cálculo:**
        - **Peticiones Aprobadas:** Recalculan todas las horas ✅
        - **Peticiones Canceladas:** Recalculan todas las horas ✅
2. **Solicitudes automaticas**
#### 2. Eliminar peticiones
- comprobar si es autovalidada para sumar las horas a las restantes ⏰
- ASegurarse de que el sumado de horas se realiza correctamente ⏰

## Notificaciones y Comunicación
### Notificaciones:
- Al enviar una solicitud, se notifica automáticamente a los administradores. ⏰

### Chatter (Sistema de Mensajes):

- Implementado en todos los módulos. ✅
- **Funcionalidad:** Registra automáticamente los cambios en solicitudes y cálculos dentro del chatter. ✅

## Grupos de Permisos
1. **Primer Aprobador:**
    - Cada usuario tiene asignado un primer aprobador. ✅
    - Los aprobadores solo pueden aprobar las solicitudes de las personas que gestionan, no las propias. ✅
2. **Segundo Aprobador:**
    - Existe un segundo nivel de aprobación con permisos específicos para revisar solicitudes ya aprobadas por el primer aprobador. ⏰



---
**Administracion permisos de visualizacion**
> Estamos desarrollando un sistema en odoo para solicitar horas extra mediante peticiones. Las peticiones tienen primera y segunda validacion. Cada empleado tiene asignado a un responsable de validacion de horas. Tras la aprobación de la peticion por el responsable, tenemos que esperar a la aprobacion del administrador. El modelo "calculo" almacena las asistencias de un empleado. Se crea un registro por dia de trabajo del empleado. Desde este modelo podemos crear peticiones de horas libres, que deberan ser aprobadas por nuestro aprobador y después por el administrador. Cuando entramos al modelo calculo podemos ver todos nuestros fichajes en ese dia y crear o acceder al listado de peticiones ya creadas para ese mismo dia (por ejemplo: si hemos trabajado 2 horas extra, creariamos la peticion desde este modelo y se crearia un nuevo registro en el modelo de peticiones). Las restricciones son las siguientes: - Las peticiones unicamente pueden ser vistas por: - El solicitador de la peticion - El aprobador del que solicita la peticion - El administrador, que tiene acceso a todos los registros. - Los registros del modelo calculo solo pueden ser vistos por: - El propio usuario dueño del registro - El administrador

**Calculo de horas extra**
>Estamos trabajando en un modelo de odoo que nos permite llevar un registro de las asistencias y de las horas extra de un trabajador.
>Los trabajadores tienen un horario de trabajo diario asignado (8am a 4pm)
>Los trabajadores pueden enviar peticiones de horas extra en la que indican de que hora a que hora han hecho horas extra. La peticion puede mostrar solo el tramo extra que han realizado extra, o todo el dia completo. por ejemplo: peticion de 7am a 6pm o peticion de 7am a 8am y de 4pm a 6pm
>
>Las horas extra son de tipo:
> - extra normal (cuando se ecceden las horas de trabajo de la jornada diaria)
> - extra festiva (cuando se realizan horas de trabajo en dias festivos)
> - extra nocturna (cuando se realizan horas de trabajo dentro de horario nocturno 8pm a 8am).



```md
Estamos trabajando en un modelo de odoo que nos permite llevar un registro de las asistencias y de las horas extra de un trabajador.

Los trabajadores tienen un horario de trabajo diario asignado (8am a 4pm)

Los trabajadores pueden enviar peticiones de horas extra en la que indican de que hora a que hora han hecho horas extra.

Si el trabajador ha hecho de 7am a 6pm, la peticion puede mostrar solo el tramo extra que han realizado extra, o todo el dia completo. por ejemplo: peticion de 7am a 6pm o peticion de 7am a 8am y de 4pm a 6pm

Las horas extra son de tipo:

- hora extra (cuando se ecceden las horas de trabajo de la jornada diaria)

- hora en festivo (cuando se realizan horas de trabajo en dias festivos)

- hora nocturna (cuando se realizan horas de trabajo dentro de horario nocturno 8pm a 8am).

Los tipos de horas extra se pueden combinar. Nuestro objetivo es saber de una o un conjunto de peticiones de horas extra de un empleado en un mismo dia, el numero total de horas de cada uno de los siguientes tipos:

- hora extra

- hora en festivo

- hora en nocturno

- hora extra en festivo

- hora extra en nocturno

- hora extra en festivo y nocturno

Las horas extra se han de contar siempre desde el final de la jornada. Para nuestro ejemplo:

siendo un dia festivo

Horario nocturnidad de 8am a 8pm

horario de trabajo diario asignado (7am a 3pm)

horario trabajado: 7am a 11pm

El trabajador debera de tener ese dia:

1 hora de festivo nocturno de 7am a 8pm

7 horas de festivo de 8 a 3pm

5 horas extra en festivo de 15pm a 8pm

3 horas extra en festivo y nocturno de 8pm a 11pm
```

> [[https://github.com/puntsistemes/palacio-congresos_odoo/pull/24/files]]


stock.move

```  
class StockRule(models.Model):  
    _inherit = "stock.rule"  
    def _get_stock_move_values(  
            self,  
            product_id,  
            product_qty,  
            product_uom,  
            location_id,  
            name,  
            origin,  
            company_id,  
            values,  
    ):  
        res = super(StockRule, self)._get_stock_move_values(  
            product_id,  
            product_qty,  
            product_uom,  
            location_id,  
            name,  
            origin,  
            company_id,  
            values,  
        )  
        if values.get("sale_line_id", False):  
            sale = self.env['sale.order.line'].browse(  
                values.get('sale_line_id'))  
            res["pnt_purchase_price"] = sale.purchase_price  
            res["description_picking"] = sale.name

        return res  
```

stock.move.line

```  
class StockMove(models.Model):  
    _inherit = "stock.move"

     def _prepare_move_line_vals(self, quantity=None, reserved_quant=None):  
        res = super()._prepare_move_line_vals(  
            quantity=quantity, reserved_quant=reserved_quant  
        )  
        if res.get("move_id", False):  
            move = self.env["stock.move"].browse(res.get("move_id", False))  
            if move:  
                res.update({"pnt_description": move.description_picking})  
        return res  
```

Para la cabecera

```  
def _get_new_picking_values(self):  
    vals = super()._get_new_picking_values()  
    sale_note = self.sale_line_id.order_id.picking_note  
    if sale_note:  
        vals['note'] = sale_note  
    return vals  
```