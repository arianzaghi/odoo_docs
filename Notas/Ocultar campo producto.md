> [[Albaran (ALB)]]

Tags: 
Status: 
Related: 

___

# Ocultar campo producto

```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="pnt_report_invoice_document" inherit_id="stock.report_delivery_document">  
        <!-- Ocultar columna producto SM (Cabecera y Cuerpo-->  
        <xpath expr="//th[@name='th_sm_product']" position="attributes">  
            <attribute name="t-if">False</attribute>  
        </xpath>  
        <xpath expr="//td[//span[@t-field='move.product_id']]" position="attributes">  
            <attribute name="t-if">False</attribute>  
        </xpath>  
        
        <!-- Ocultar columna producto SML (Cabecera)-->  
        <xpath expr="//th[@name='th_sml_product']" position="attributes">  
            <attribute name="t-if">False</attribute>  
        </xpath>  
    </template>  
    
    <template id="pnt_stock_report_delivery_has_serial_move_line">  
        <!-- Ocultar columna producto SML (Cuerpo)-->  
        <xpath expr="//td[//span[@t-field='move_line.product_id']]" position="attributes">  
            <attribute name="t-if">False</attribute>  
        </xpath>  
    </template>  
</odoo>
```