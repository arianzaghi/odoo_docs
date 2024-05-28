> [[Back]]

Tags: 
Status: 
Related: 

___

# Dividir carga cuando tenemos muchos registros (200.000+)

```python
from odoo.tools.misc import split_every

for moves_chunk in split_every(100, entry_moves.ids):
    moves = self.browse(moves_chunk).sudo()

    for move in moves:
        partner = move.partner_id
    
    
    self.env.cr.commit()
        
```