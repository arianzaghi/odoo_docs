> [[Pedido de Venta (PV)]]

Tags: 
Status: 
Related: 

___

# Payment Mode Saleorder

## `sale_report_templates.xml`
> `bank-payment/account_payment_sale/views/`
```xml
<?xml version="1.0" encoding="utf-8" ?>  
<odoo>  
    <template id="report_sale_payment_mode" inherit_id="sale.report_saleorder_document">  
        <xpath  
            expr="//p[@t-if='not is_html_empty(doc.payment_term_id.note)']"  
            position="after"  
        >  
            <p  
                t-if="not is_html_empty(doc.payment_mode_id.note)"  
                id="payment_mode_note"  
            >  
                <strong>Payment Mode:</strong>  
                <span t-field="doc.payment_mode_id.note" />  
            </p>  
        </xpath>  
    </template>  
</odoo>
```