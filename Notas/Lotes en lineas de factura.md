> [[Factura (FRA)]]

Tags: 
Status: 
Related: 

___

# Lote en lineas de factura

> **Objetivo:** Mostrar en lineas de factura todos los lotes que se han usado junto a las cantidades de cada lote.

> [!DANGER] Importante
> Solo se puede usar este método cuando tenemos instalado `grouped_by_picking`

![[Pasted image 20250602130513.png]]

![[Pasted image 20240502172804.png]]

## Metodos sin programacion
> Podemos encontrar los lotes desde las lineas de albaran directamente (sencillo) o desde las lineas de venta (avanzado)
### Sencillo
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="pnt_report_invoice_document"  
              inherit_id="account.report_invoice_document">  
              
        <xpath expr="//td[@name='account_invoice_line_name']" position="inside">  
            <t t-if="o.move_type == 'out_invoice' and o.state == 'posted'"  
               class="text-center">  
               
                <span t-esc="','.join(line.move_line_ids.mapped('lot_ids.name'))"/>  
                <span t-esc="','.join(line.move_line_ids.mapped('qty_done'))"/>  
                
            </t>  
        </xpath>  
    </template>  
</odoo>
```

### Avanzado (Gonzalo)
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="pnt_report_invoice_document"  
              inherit_id="account.report_invoice_document">  
        <xpath expr="//td[@name='account_invoice_line_name']" position="inside">  
            <t t-if="o.move_type == 'out_invoice' and o.state == 'posted'"  
               class="text-center">  
               
                <t t-foreach="line.sale_line_ids.mapped('move_ids.move_line_ids')"  
                   t-as="move_line">  
                    <t t-if="move_line.lot_id">  
                        <div>  
                            <t t-if="move_line.qty_done">  
                                <span>S/N:  
                                    <t t-esc="move_line.lot_id.name"/>  
                                </span>  
                                <t t-esc="int(move_line.qty_done)"/>  
                            </t>  
                        </div>  
                    </t>  
                </t>  
            </t>  
        </xpath>  
    </template>  
</odoo>
```
## Metodo con Programación
> [Aditivos v16 - Miquel](https://github.com/puntsistemes/aditivos_odoo/commit/98fc81a2424af8769bfa2d8c4e29def35c28670c)
> [Usisa v17 - Arian](https://github.com/puntsistemes/usisa_odoo/pull/11)
> Python en los commits
```xml
<xpath expr="//table//td[@name='account_invoice_line_name']" position="before">
	<td name="td_lot" style="white-space: nowrap;
						overflow: hidden;
						text-overflow: ellipsis;">
		<t t-foreach="lines_group['lot_values']" t-as="lot_value">
			<span t-esc="lot_value['lot']"/>
			<br/>
		</t>
	</td>

	<td name="td_client_ref"><span t-esc="line.product_id.pnt_get_client_ref(o.partner_id)"/></td>
	<td name="td_prod_code"><span t-field="line.product_id.default_code"/></td>
	<td name="td_packaging_qty" style="white-space: nowrap;
						overflow: hidden;
						text-overflow: ellipsis;">
		<t t-foreach="lines_group['lot_values']" t-as="lot_value">
			<span t-esc="lot_value['qty']"/>
			<br/>
		</t>
	</td>
</xpath>
```