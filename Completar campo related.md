> [[|Back]]

Tags: 
Status: 
Related: [[related]]

___

# Completar campo related

1. Identificamos los modelos que queremos vincular (A y B).
2. Navegamos dentro de Odoo a los campos del modelo A.
3. **Ajustes > Técnico > Estructura de la base de datos > Modelos > A**
	1. Buscamos [[Many2one|un campo Many2one]] que vincule con el modelo B.
	2. Utilzamos la conexión entre modelos a través de estos campos para obtener datos del modelo B en el modelo A.

> [!NOTE]
> Si utilizamos un campo One2may o Many2many, recibiriamos en lugar de 1 valor, una lista de valores procedentes del lado "many" de la relación.


## Ejemplo

1. Objetivo:
	- Rellenar el campo related
	- Obtener desde `stock.move.line` (A) el id del empaquetado del producto localizado en `sale.order.line`(B)

```python
class StockMoveLine(models.Model):  
    _inherit = "stock.move.line"

product_packaging_id = fields.Many2one(  
    string="Packaging",  
    comodel_name='product.packaging',  
    related= # TODO
    store=True,  
)
```

2. Navegamos al listado de campos del modelo `stock.move.line` (A).
3. Buscamos el campo relacional de `stock.move.line` (A), que vincule con `sale.order.line` (B) o con un modelo intermediario entre ambos.
   
![[Pasted image 20231212161609.png]]
![[Pasted image 20231212161526.png]]
5. Navegamos al listado de campos de `stock.move` y buscamos alguno que conecte con el modelo `sale.order.line`, o con alguno intermediario entre ambos.

   
![[Pasted image 20231212161005.png]]
![[Pasted image 20231212161220.png]]

> [!NOTE] Nota
> El campo relacional que vincula el modelo A con el B, no aparecerá en el listado de campos del modelo B.


6. El campo `sale_line_id` vincula `stock.move` con `sale.order.line`. Ya hemos completado el camino del related.
7. Resultado final:
   
```python
class StockMoveLine(models.Model):  
    _inherit = "stock.move.line"

product_packaging_id = fields.Many2one(  
    string="Packaging",  
    comodel_name='product.packaging',  
    related= 'move_id.sale_line_id.product_packaging_id'
    store=True,  
)
```

>[!WARNING] Cuidado!
>Es importante añadir en el `depends` de nuestro módulo de odoo, todos los modelos por los que hayamos pasado para hacer la conexión entre A y B.
