> [[Informes XML]]

Tags: 
Status: 
Related: 

___

# Heredar de un template de invocación de informe

```xml
<template id="custom_report_invoice_with_payments"
          inherit_id="account.report_invoice_with_payments">
    <xpath expr="//t[@t-call='account.report_invoice_document']" position="replace">
        <t t-if="o.company_id.id != 53">
            <t t-if="o._get_name_invoice_report() == 'account.report_invoice_document'"
               t-call="account.report_invoice_document" t-lang="lang"/>
        </t>
        <t t-if="o.company_id.id == 53">
            <t t-if="o._get_name_invoice_report() == 'account.report_invoice_document'"
               t-call="report_pnt.report_custom_invoice_document" t-lang="lang"/>
        </t>
    </xpath>
</template>
```