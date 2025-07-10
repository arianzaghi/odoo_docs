> [[Añadir datos a informe]]

Tags: 
Status: 
Related: 

___

# Plazo pago, modo pago, datos bancarios informes

## 1. Factura

```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="pnt_report_invoice_document"  
              inherit_id="account.report_invoice_document">
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
            <span                t-esc="o.partner_id.bank_ids[0].acc_number[:(len(o.partner_id.bank_ids[0].acc_number)-4)] + '*' * 4"/>  
            <p t-if="o.partner_id.bank_ids.bank_id">  
                <span class="o_report_layout" style="font-weight:bold;">Número BIC o Swift:</span>  
                <span t-field="o.partner_id.bank_ids[0].bank_id"/>  
            </p>        </p>        <p t-if="o.payment_mode_id" name="payment_mode">  
            <span style="font-weight:bold;">Modo de pago:</span>  
            <span t-field="o.payment_mode_id"/>  
        </p>  
        <p t-if="o.invoice_payment_term_id" name="payment_term_id">  
            <span style="font-weight:bold;">Plazo de pago:</span>  
            <span t-field="o.invoice_payment_term_id"/>  
        </p>    </xpath></template>
```

## 2. Pedido de Venta

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<odoo>  
    <template id="report_sale_order_document_pnt" inherit_id="sale.report_saleorder_document">
        <!--Para evitar duplicados deshabilitamos la vista de la OCA: account_payment_partner.report_invoice_payment_mode-->  
        <p t-if="doc.payment_mode_id.fixed_journal_id.bank_account_id and doc.payment_mode_id.name!='GIRO'"  
           name="bank_acc">  
            <span style="font-weight:bold;">Cuenta bancaria:</span>  
            <span t-field="doc.payment_mode_id.fixed_journal_id.bank_account_id"/>  
        </p>  
        <p t-if="doc.payment_mode_id and doc.partner_id.bank_ids and doc.payment_mode_id.name=='GIRO'">  
            <span class="o_report_layout" style="font-weight:bold;">Cuenta bancaria:</span>  
            <span                t-esc="doc.partner_id.bank_ids[0].acc_number[:(len(doc.partner_id.bank_ids[0].acc_number)-4)] + '*' * 4"/>  
            <p t-if="doc.partner_id.bank_ids.bank_id">  
                <span class="o_report_layout" style="font-weight:bold;">Número BIC o Swift:</span>  
                <span t-field="doc.partner_id.bank_ids[0].bank_id"/>  
            </p>        </p>    </xpath></template>
```