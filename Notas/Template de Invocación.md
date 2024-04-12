> [[Informes XLM]]

Tags: 
Status: 
Related: 

___

# Template de invocación

```xml
<template id="pnt_report_deliveryslip">  
    <t t-foreach="docs" t-as="o">  
        <t t-call="stock.report_delivery_document" t-lang="o._get_report_lang()"/>  
    </t>  
</template>
```