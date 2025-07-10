> [[Factura (FRA)]]

Tags: 
Status: 
Related: 

___

# Poner datos entrega factura en negrita

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<odoo>  
    <template id="pnt_report_invoice_document" inherit_id="account.report_invoice_document">
    
<!-- Dirección del cliente en negrita -->  
<xpath expr="//address[@t-field='o.partner_id']" position="attributes">  
    <attribute name="class">mb-0 fw-bold</attribute>  
</xpath>  
  
<!-- Dirección del cliente en negrita -->  
<xpath expr="//div[@name='address_same_as_shipping']//address[@t-field='o.partner_id']" position="attributes">  
    <attribute name="class">mb-0 fw-bold</attribute>  
</xpath>  
  
<!-- Dirección de envío en negrita -->  
<xpath expr="//div[@t-field='o.partner_shipping_id']" position="attributes">  
    <attribute name="class">fw-bold</attribute>  
</xpath>  
  
<!-- Contenedor VAT (cuando dirección = envío) -->  
<xpath expr="//div[@id='partner_vat_address_same_as_shipping']" position="attributes">  
    <attribute name="class">fw-bold</attribute>  
</xpath>  
  
<!-- Contenedor VAT (cuando dirección ≠ envío) -->  
<xpath expr="//div[@id='partner_vat_address_not_same_as_shipping']" position="attributes">  
    <attribute name="class">fw-bold</attribute>  
</xpath>  
  
<!-- Contenedor VAT (cuando no hay dirección de envío) -->  
<xpath expr="//div[@id='partner_vat_no_shipping']" position="attributes">  
    <attribute name="class">fw-bold</attribute>  
</xpath>  
  
<!-- Etiqueta Shipping Address en negrita -->  
<xpath expr="//strong[@class='d-block mt-3']" position="attributes">  
    <attribute name="class">d-block mt-3 fw-bold</attribute>  
</xpath>
```