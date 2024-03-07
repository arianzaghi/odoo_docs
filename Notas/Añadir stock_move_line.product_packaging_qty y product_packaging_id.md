> [[stock.move.line]]

Tags: 
Status: 
Related: 

___

# Añadir pnt_product_packaging_qty

```python
class StockMoveLine(models.Model):  
    _inherit = "stock.move.line"  
  
    pnt_product_packaging_qty = fields.Integer(  
        string="Packaging Qty",  
        compute='_compute_product_packaging_qty',  
        readonly=True  
    )  
  
    pnt_product_packaging_id = fields.Many2one(  
        string="Packaging",  
        comodel_name='product.packaging',  
        related='move_id.sale_line_id.product_packaging_id',  
        store=True,  
    )  
  
    def _compute_product_packaging_qty(self):  
        for line in self:  
            line.pnt_product_packaging_qty = math.ceil(  
                line.qty_done / line.pnt_product_packaging_id.qty) if line.pnt_product_packaging_id.qty > 0 else 0
```