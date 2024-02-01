>[[Campos relacionales|Back]]

Tags: #
Related: 

___

# Many2one

## **Descripcion**

Las relaciones "many2one" en Odoo permiten establecer una conexión de muchos a uno entre dos modelos. Esto implica que varios registros de un modelo pueden estar asociados a un solo registro en otro modelo.

## **Sintaxis:**

```python
field_name = fields.Many2one('related.model', string='Field Label', [optional_parameters])
```

- `field_name`: El nombre del campo en el modelo actual. (Many)
- `'related.model'`: El nombre del modelo con el que se establecerá la relación. (One)
- `string='Field Label'`: Una etiqueta opcional para el campo que se mostrará en la interfaz de usuario.
- [[#^878133|[optional_parameters]]]: Parámetros adicionales como `ondelete` para especificar el comportamiento en caso de eliminación.

## **Ejemplos:**

### Ejemplo 1

```python
class SaleOrder(models.Model):
    _name = 'sale.order'
    
    partner_id = fields.Many2one('res.partner', string='Customer', ondelete='set null', index=True)

```

En este ejemplo, la relación many2one se establece entre el modelo `sale.order` y `res.partner`. Cada orden de venta (`sale.order`) está asociada a un único cliente (`res.partner`). La etiqueta en la interfaz de usuario para este campo será 'Customer', y en caso de eliminación del cliente, el campo se establecerá en nulo (`ondelete='set null'`).

### Ejemplo 2

Supongamos que tenemos dos modelos, `ParentModel` y `ChildModel`, y queremos crear una relación de muchos a uno desde `ChildModel` a `ParentModel`:

```python
class ParentModel(models.Model):
    _name = 'parent.model'
    name = fields.Char(string='Nombre')

class ChildModel(models.Model):
    _name = 'child.model'
    parent_id = fields.Many2one('parent.model', string='Padre')
    child_name = fields.Char(string='Nombre del Hijo')
```

En este ejemplo, el modelo `ChildModel` tiene un campo `Many2one` (`parent_id`) que se refiere al `ParentModel`.
## Optional Parameters

^878133

- **comodel_name:**
	  Nombre del modelo objetivo. Obligatorio excepto para campos relacionados o extendidos.

- **[[domain]]:**
	  Un dominio opcional para establecer en los valores candidatos en el lado del cliente (dominio o cadena).

- **context (dict):**
	  Un contexto opcional para usar en el lado del cliente al manejar ese campo.

- **ondelete (str):**
	  Qué hacer cuando se elimina el registro referenciado; los valores posibles son: 'set null', 'restrict', 'cascade'.

- **auto_join (bool):**
	  Si se generan JOINs durante la búsqueda a través de ese campo (predeterminado: False).

- **delegate (bool):**
	  Establézcalo en True para hacer que los campos del modelo objetivo sean accesibles desde el modelo actual (corresponde a _inherits).

- **check_company (bool):**
	  Marca el campo para ser verificado en _check_company(). Agrega un dominio de empresa predeterminado según los atributos del campo.
