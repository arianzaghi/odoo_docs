Tags: #xml
Status: 
Related: 

___

# Xpath

## **Descripción**

XPath is a query language that enables the selection of nodes in an XML document. In Odoo, XML is extensively used for defining views, reports, and data structures.

## Sintaxis

- **Selecting Nodes:** Selects all partner nodes
    `//partner`
    
- **Attribute Selection:** Selects partner nodes with the name attribute equal to 'John'
	`//partner[@name='John']`

- **Path Steps:** Selects address nodes under partner nodes
    `//partner/address`
    
- **Wildcards:** Selects all child nodes under partner
    `//partner/*`

- **Field Selection in Views:** Selects the field with the name 'amount_total' in a view
    `//field[@name='amount_total']`
    
- **Domain Filtering:** Filters sale order records with 'draft' state
    `//record[@model='sale.order'][('state','=','draft')]`

- **Field Positioning:** Selects the field following 'date_order' in a view
    `//field[@name='date_order']/following-sibling::field`
    
- **Conditional Rendering:** Applies a widget when the state is 'done'
    `//field[@name='state'][('state','=','done')]/widget`