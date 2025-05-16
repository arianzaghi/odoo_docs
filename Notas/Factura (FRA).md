> [[Lista de informes XML]]

Tags: 
Status: 
Related: 

___

# Factura (FRA)

> `/opt/sources/odoo170/src/core/addons/account/views/report_invoice.xml`
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