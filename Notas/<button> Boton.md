> [[Etiquetas XML]]

Tags: 
Status: 
Related: 

___

# `<button>`

La etiqueta XML `button` en Odoo proporciona desencadena acciones, llama a métodos y maneja atributos dinámicos basados en valores de registros.

## Relacionado

- [[botones colores]]
- [[boton que llama a un metodo]]
- [[Botones en proyecto para ver documentos relacionados]]
- [[Buscar boton javascript]]
- [[Stat button]]

## Atributos

### 1. `icon`

- Icono que se mostrará en el botón.
- Utilizamos la galería de iconos "[Font Awesome](https://fontawesome.com/icons)"
### 2. `type`

- Especifica el tipo de botón y define su comportamiento.
- **Valores posibles:**
    - `object`
	    Llama a un método en el modelo actual. El nombre del botón es el método, que se llama con el ID del registro actual y el contexto actual.
    - `action`
	    Carga y ejecuta una `ir.actions`. El `name` del botón es el ID de la acción en la base de datos. El contexto se expande con `active_model`, `active_id` y `active_ids`.

### 3. `name`

- Relevante para el atributo `tipo`, especifica el **método o acción a ejecutar.**

### 4. `args`

- Relevante para el atributo `tipo`, proporciona **argumentos adicionales para el método o acción**.

### 5. `attrs`

- Atributos dinámicos basados en valores de registros.
- **Atributos:**
    - `invisible`: Oculta el botón si se cumple la condición especificada.

### 6. `states`

- Forma abreviada para atributos `invisible`. Oculta el botón según el estado del registro.
- **Nota:** El uso de `estados` en combinación con `attrs` puede dar lugar a resultados inesperados, ya que los dominios se combinan con un AND lógico.

### 7. `context`

- **Descripción:** Contexto en el que opera el botón.

## 8. `confirm`

^882255
- Wizard o mensaje popup de confirmación (aceptar o cancelar) antes de que se realize la acción del botón
- [[popup confirmación]]

## 9. `special`

- Para formularios abiertos en diálogos
- `save` para guardar y cerrar. `cancel` para cerrar y descartar.

## Ejemplo de Uso

```python
<button
    icon="fa-cogs"
    type="object"
    name="realizar_accion"
    args="['arg1', 'arg2']"
    attrs="{'invisible': [('campo', '=', False)]}"
    estados="borrador,confirmado"
    contexto="{'clave': 'valor'}",
    confirm = '¿Estas seguro que deseas continuar?'
/>
```