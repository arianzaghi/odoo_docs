> [[Modificaciones comunes XLM]]

Tags: 
Status: 
Related: 

___

# Ocultar nombre comercial direccion de entrega o datos cliente

```xml
<t t-set="information_block">  
    <div class="row">  
        <div class="col-8">  
            <strong>  
                <t t-if="doc.partner_shipping_id == doc.partner_invoice_id">  
                    Invoicing and Shipping Address:  
                </t>  
                <t t-else="">  
                    Invoicing Address:  
                </t>  
            </strong>  
            <div t-field="doc.partner_id.name"/>  
            <div t-field="doc.partner_invoice_id"  
                 t-options='{"widget": "contact", "fields": ["address", "phone"], "no_marker": True, "phone_icons": True}'
			 />  
		 </div>
	</div>
</t>
```