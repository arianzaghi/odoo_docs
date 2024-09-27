> [[Albaran (ALB)]]

Tags: 
Status: 
Related: 

___

# Marcar devoluciones en lineas de albarán

> "Albarán de compra con devolución"
> Historia de Urban donde se solicita poner un check en cada línea que tenga una devolución. Desde el purchase.order.line, se va a los albaranes, se filtra por los albaranes de devolución hechos y se busca la línea del purchase.order.line relacionada

```python
    pnt_line_return = fields.Boolean(  
        string="Picking with return",  
        compute="_compute_pnt_return",  
    )

    def _compute_pnt_return(self):  
        for record in self:  
            returned_pickings = record.mapped('move_ids.returned_move_ids')  
            if not returned_pickings:  
                record.pnt_line_return = False  
                continue  
            done_pickings = returned_pickings.filtered(lambda p: p.state == 'done')  
            if not done_pickings:  
                record.pnt_line_return = False  
                continue  
            origin_return = done_pickings.mapped("origin_returned_move_id")  
            line_return = origin_return.mapped("purchase_line_id")  
            record.pnt_line_return = bool(line_return)
```