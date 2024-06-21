> [[Modificaciones comunes XML]]

Tags: #informe
Status: 
Related: [[account.move]]

___

# Mostrar datos bancarios cliente

> [Aditivos_47392](https://github.com/puntsistemes/aditivos_odoo/commit/16be58f06be6ebb8e31cd60ef6d022d6a3f43ad3#diff-2677e5acc6af7f548dbb3bba7ed69890da79d310d66fe2db5772de6918e082de)
> Desde `account.move` mostrar en un reporte datos de la cuenta bancaria del cliente (nombre, bic, cuenta) cuando el tipo de pago es 'GIRO'


```python
<xpath expr="//p[@t-if='o.payment_mode_id.note and False']" position="after">
	<div t-if="o.payment_mode_id.note" name="pnt_payment_mode">
		<t t-set="bank_name" t-value="o.partner_id.bank_ids[0].bank_id.name or ''"/>
		<t t-set="bic" t-value="o.partner_id.bank_ids[0].bank_id.bic or ''"/>
		<t t-set="acc_number" t-value="o.partner_id.bank_ids[0].acc_number or ''"/>
		<t t-set="payment_mode" t-value="o.payment_mode_id.note  or ''"/>
		<t t-set="is_giro" t-value="o.payment_mode_id.note == 'GIRO'"/>
		<t t-set="partner" t-value="o.partner_id.parent_id or o.partner_id"/>
		
		<t t-if="is_giro and partner.bank_ids">
			<t t-set="bank_name" t-value="partner.bank_ids[0].bank_id.name or ''"/>
			<t t-set="bic" t-value="partner.bank_ids[0].bank_id.bic or ''"/>
			<t t-set="acc_number" t-value="partner.bank_ids[0].acc_number or ''"/>
		</t>
		
		<strong>Payment Mode:</strong>
		<span t-esc="payment_mode"/>
		<span t-if="is_giro" t-esc="bank_name + ' (' + bic + ') ' + acc_number" />
		<span t-if="is_giro and partner.bank_ids" t-esc="bank_name + ' (' + bic + ') ' + acc_number" />
		
	</div>
	<div t-field="o.invoice_payment_term_id.note" name="pnt_payment_term"/>
</xpath>
```

- Seleccionamos la primera cuenta bancaria disponible del cliente (de la relación One2many).
- Si el cliente (partner_id) pertenece a una **empresa matriz**, utilizaremos la primera cuenta bancaria disponible de la **empresa matriz**