> [[Back]]

Tags: 
Status: 
Related: 

___

# Packing List

Informe que se imprime desde `stock.picking`

- State != 'done'
	El informe usa `stock.move`
	
- State = 'done'
	El informe usa `stock.move.line`

> [Coralim v16](https://github.com/puntsistemes/coralim_odoo/pull/34)