> [[Albaran Valorado]]

Tags: 
Status: 
Related: 

___

# Sacar fecha de texto de agrupacion por albaran

![[Pasted image 20240514105836.png]]

![[Pasted image 20240514105854.png]]

https://github.com/puntsistemes/intoolges_odoo/pull/13/files#diff-2677e5acc6af7f548dbb3bba7ed69890da79d310d66fe2db5772de6918e082de

## Version ARIAN

### `report_invoice.xml`
```xml
<template id="report_invoice_document_pnt" inherit_id="account_invoice_report_grouped_by_picking.report_invoice_document">  
    <xpath expr="//t//tr[@t-if='picking']//td[@colspan='10']" position="after">  
        <td colspan="10">  
            <strong>  
                <span>Picking:</span>  
                <span t-field="picking.name"/>  
                <span>Order:</span>  
                <span t-field="picking.sale_id.name"/>  
                <t t-if="picking.sale_id.client_order_ref">  
                    <span t-translation="off">(</span>  
                    <span t-field="picking.sale_id.client_order_ref"/>  
                    <span t-translation="off">)</span>  
                </t>  
                <span>Date:</span>  
                <span  
                    t-field="picking.date_done"  
                    t-options="{'widget': 'date'}"  
                />  
            </strong>  
        </td>  
    </xpath>  
    <xpath expr="//t//tr[@t-if='picking']//td[@colspan='10']" position="attributes">  
        <attribute name="t-if" add="False" separator=" and "/>  
    </xpath>  
</template>
```