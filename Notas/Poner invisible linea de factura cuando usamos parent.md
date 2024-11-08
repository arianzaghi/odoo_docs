> [[Factura (FRA)]]

Tags: 
Status: 
Related: 

___

# Poner invisible linea de factura en base al estado de la fra

> Cuando queremos ocultar una columna de las lineas del tree, debemos hacerlo para todas o para ninguna.
> 
> Para encontrar el factor común entre las lineas, nos vamos al parent (la cabecera de la factura) y usamos uno de sus campos junto al attribute `column_invisible` en vez de simplemente `invisible` para ocultar esta columna en todas las lineas

```xml
<field attrs="{'column_invisible': [('parent.move_type', 'not in', ['in_refund','in_invoice'])]}"/>
```



```xml
<xpath expr="//field[@name='line_ids']//tree" position="inside">  
    <field
	    name="pnt_picking_supplier_id"
	    attrs="{'column_invisible': [('parent.move_type', 'not in', ['in_refund','in_invoice'])]}"
    />  
    <field name="pnt_stock_picking_ids" invisible="1"/>  
</xpath>
```