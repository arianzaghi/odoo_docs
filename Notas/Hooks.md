> [[Python framework]]

Tags: 
Status: 
Related: 

___

# Hooks

Permiten sobrescribir métodos pertenecientes al core de forma que se ejecute el nuestro en lugar del original.

## Existen 3 tipos de hooks:

- post_load_hook()
- post_init_hook()
- pre_init_hook()

## Configuración hook

1. Creamos fichero `hooks.py` en la **raíz** del modulo en cuestión (`custom_pnt`)
2. Lo añadimos al `__init__.py` y al `__manifest__.py`

### Dentro de `hooks.py

1. Importamos el módulo/s de odoo que vamos a sobrescribir
````python
from odoo.addons.MODULO.models.MODELO import NombreDeLaClase

#Ejemplo con stock:
from odoo.addons.stock.models.stock_move_line import StockMoveLine
````

2. Creamos el método del tipo de [[Hooks#Existen 3 tipos de hooks|hooks]] que vamos a usar
````python
def post_load_hook():  
    def _get_aggregated_product_quantities(self, **kwargs):
	    pass
````

3. Indicamos la función que vamos a reemplazar en el modelo original

````python
StockMoveLine._patch_method("_get_aggregated_product_quantities", _get_aggregated_product_quantities)
````

### Manifest
Añadimos el hook al manifest


Referencia: https://github.com/puntsistemes/cafes-minyana_odoo/blob/14.0/custom_pnt/hooks.py