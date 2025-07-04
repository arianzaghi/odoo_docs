> [[040 - Python framework]]

Tags: 
Status: 
Related: 

___

# Hooks

Permiten sobrescribir métodos pertenecientes al core de forma que se ejecute el nuestro en lugar del original.


> [!WARNING] Aviso
> En v17 es distinto como se usan los hook

## Tipos de hooks:

Existen 3 tipos de `hooks`
1. post_load_hook()
2. post_init_hook()
3.  pre_init_hook()

## Configuración hook

### 1. Creamos fichero `hooks.py` en la **raíz** del modulo en cuestión (`custom_pnt`)
![[Pasted image 20240520114956.png]]
### 2. Importamos la función del hook en el `__init__.py`

**`__init__.py`**
```python
from .hooks import post_load_hook
```

### 1. Importamos la función en el manifest usando el parámetro `post_load`

**`__manifest__.py`**
```python
{
    "name": "...",
    "post_load": "post_load_hook",
    "depends": [
        "...",
    ],
    "data": [
        "...",
    ],
}
```

### Dentro de `hooks.py

#### 1. Importamos el módulo/s de odoo que vamos a sobrescribir
````python
from odoo.addons.MODULO.models.MODELO import NombreDeLaClase

#Ejemplo con stock:
from odoo.addons.stock.models.stock_move_line import StockMoveLine
from odoo.addons.account.models.account_move import AccountMove
````

#### 2. Creamos el método del tipo de [[Hooks#Existen 3 tipos de hooks|hooks]] que vamos a usar
````python
def post_load_hook():  
    # Metodo que queremos hookear aqui
````

3. Dentro de nuestro método, añadimos:

#### **Metodo que queremos hookear aqui**
```python
def _get_aggregated_product_quantities(self, **kwargs):
	pass
```

#### **Indicamos la función que vamos a reemplazar en el modelo original**
````python
StockMoveLine._patch_method("_get_aggregated_product_quantities", _get_aggregated_product_quantities)
````

> [!WARNING] AVISO
> En v17, ya no existe patch_method. Tenemos que usar:
> ```
>     SaleOrderLine._compute_discount =_compute_discount
> ```



### Manifest
Añadimos el hook al manifest

## Ejemplos

### Post Load Hooks

#### [Aditivos - Arian](https://github.com/puntsistemes/aditivos_odoo/pull/23/files#diff-c8299e4fab78b67992dc0abdcbb93292d43b3616dcc02aa58ddcca49b46f688e)
#### [Minyana - Juanma](https://github.com/puntsistemes/cafes-minyana_odoo/blob/14.0/custom_pnt/hooks.py)
#### Argui - Arian
> El core calcula un descuento en base a la lista de precios, y el modulo OCA sale_product_pack lo pisa en base al precio establecido en producto > packs > descuento.
> 
> Queremos modificar el metodo de OCA para que si ya viene la linea con descuento, no la modifique.

```python
from odoo import api  
from odoo.addons.sale_product_pack.models.sale_order_line import SaleOrderLine  
  
  
def post_load_hook():  
    @api.depends("product_id", "product_uom", "product_uom_qty")  
    def _compute_discount(self):  
        res = super(SaleOrderLine, self)._compute_discount()  
        for pack_line in self.filtered("pack_parent_line_id"):  
            if not pack_line.discount:  
                pack_line.discount = pack_line._get_pack_line_discount()  
        return res  
  
    SaleOrderLine._compute_discount =_compute_discount
```

#### EN v17
> ![[Pasted image 20240909165318.png]]
> Se pone la clase.método = nuevo_método
> 
> 
> 
> Hook para reemplazar método de la OCA. Se aplica a varios clientes
> 
> [[https://github.com/puntsistemes/towerdigital_odoo/pull/35]]
> 
> Se importa el módulo de la OCA (account_invoice_report_grouped_by_picking) y el modelo afectado (account_move)
> 
> ![[Pasted image 20250611124238.png]]


Luego construyes todo el código que necesitas y luego al final llamas al método nuevamente:

![[Pasted image 20250611124255.png]]

Con respecto a la estructura el manifest depende del módulo de la OCA afectado (account_invoice_report_grouped_by_picking) y el hooks.py se coloca sobre el mismo módulo (no va dentro de models ni nada)

![[Pasted image 20250611124453.png]]