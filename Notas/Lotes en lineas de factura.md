> [[Factura (FRA)]]

Tags: 
Status: 
Related: 

___

# Lote en lineas de factura

> **Objetivo:** Mostrar en lineas de factura todos los lotes que se han usado junto a las cantidades de cada lote.

> [!DANGER] Importante
> Solo se puede usar este método cuando tenemos instalado `grouped_by_piicking`

![[Pasted image 20240502172804.png]]

## Programación
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


## Ejemplos
> [Aditivos v16 - Miquel](https://github.com/puntsistemes/aditivos_odoo/commit/98fc81a2424af8769bfa2d8c4e29def35c28670c)
> [Usisa v17 - Arian](https://github.com/puntsistemes/usisa_odoo/pull/11)
