> [[Lista de informes XML]]

Tags: 
Status: 
Related: 

___

# Factura (FRA)

> `/opt/sources/odoo170/src/core/addons/account/views/report_invoice.xml`

```xml
<template id="report_invoice_document">
```
## `report_invoice.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="pnt_report_invoice_document"
		  inherit_id="account.report_invoice_document">
    </template>
</odoo>
```

### Modificar decimales cantidad y precio
> Cuando está instalado `account_invoice_report_grouped_by_picking` el modulo hereda y no permite cambiar las cantidades
> Tenemos que heredar de este modulo para cambiarlas



```xml
<template id="pnt_account_invoice_grouped_by_picking" inherit_id="account_invoice_report_grouped_by_picking.report_invoice_document">  
    <xpath expr="//td/span[@t-esc=&quot;lines_group['quantity']&quot;]" position="attributes">  
        <attribute name="t-options">{'widget': 'float', 'precision': 2}</attribute>  
    </xpath>  
</template>
```

## Modo Pago, Plazo Pago y datos bancarios

```xml
<!-- Añadimos plazo de pago, modo de pago y datos bancarios -->  
<xpath expr="//p[@name='note']" position="after">  
    <!--Para evitar duplicados deshabilitamos la vista de la OCA: account_payment_partner.report_invoice_payment_mode-->  
    <p t-if="o.payment_mode_id.fixed_journal_id.bank_account_id and o.payment_mode_id.name!='GIRO'"  
       name="bank_acc">  
        <span style="font-weight:bold;">Cuenta bancaria:</span>  
        <span t-field="o.payment_mode_id.fixed_journal_id.bank_account_id"/>  
    </p>  
  
    <p t-if="o.payment_mode_id and o.partner_id.bank_ids and o.payment_mode_id.name=='GIRO'">  
        <span class="o_report_layout" style="font-weight:bold;">Cuenta bancaria:</span>  
        <span  
            t-esc="o.partner_id.bank_ids[0].acc_number[:(len(o.partner_id.bank_ids[0].acc_number)-4)] + '*' * 4"/>  
        <p t-if="o.partner_id.bank_ids.bank_id">  
            <span class="o_report_layout" style="font-weight:bold;">Número BIC o Swift:</span>  
            <span t-field="o.partner_id.bank_ids[0].bank_id"/>  
        </p>  
    </p>  
    <p t-if="o.payment_mode_id" name="payment_mode">  
        <span style="font-weight:bold;">Modo de pago:</span>  
        <span t-field="o.payment_mode_id"/>  
    </p>  
  
    <p t-if="o.invoice_payment_term_id" name="payment_term_id">  
        <span style="font-weight:bold;">Plazo de pago:</span>  
        <span t-field="o.invoice_payment_term_id"/>  
    </p>  
</xpath>
```

[[Poner datos entrega factura en negrita]]