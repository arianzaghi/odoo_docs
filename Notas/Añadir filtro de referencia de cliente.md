> [[Search filter tree view]]

Tags:
Status: 
Related: #filtro

___

# Añadir filtro de referencia de cliente

> [Aditivos_47265](https://github.com/puntsistemes/aditivos_odoo/pull/44/commits/2b17986eae25c1801323066d7446c00d66ae527b#diff-5ad02ab088c566ec4df216c7d93979854a4fe16e84cc48dbc507e50bf9085fe7)
> Filtrar por `ref. cliente` desde `sale.order`


```python
<filter
	string="Referencia de cliente"
	name="invoice_grouping_criteria"
	domain="[]"
	context="{'group_by': 'client_order_ref'}"
/>
```