> [[Herencias comunes]]

Tags: 
Status: 
Related: 

___

# Heredar de un template que no tiene ID

Ejemplo en este [commit](https://github.com/puntsistemes/mantra-iluminacion_odoo/commit/33c6f84708553156611eee491beaf6a861e1c815#diff-0254b9e3240f8940d68b46b20ef826f166809c2f0ae010c7652479e4d829a989)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<templates>
    <t t-extend="website_sale_stock.product_availability">
        <t
            t-jquery="div[t-if*='inventory_availability == \'custom\'']"
            t-operation="after"
        >
            <div t-if="inventory_availability == 'show_and_allow'" t-attf-class="availability_message_#{product_template} text-success" t-attf-style="font-size:0.8rem !important">
                <t t-esc="virtual_available_formatted" /> stock
            </div>
        </t>
         <t
            t-jquery="t[t-esc*='uom_name']"
            t-operation="attributes"
         >
             <attribute name="t-if">False</attribute>
         </t>
         <t
            t-jquery="div[t-if*='inventory_availability == \'always\'']"
            t-operation="attributes"
        >
            <attribute name="t-attf-class">availability_message_#{product_template} text-success</attribute>
         </t>
        <t
            t-jquery="div[t-if*='inventory_availability == \'threshold\'']"
            t-operation="attributes"
        >
            <attribute name="t-attf-class">availability_message_#{product_template} text-success</attribute>
         </t>
         <t
            t-jquery="div[t-if*='inventory_availability == \'custom\'']"
            t-operation="attributes"
        >
              <attribute name="t-attf-class">availability_message_#{product_template} text-success</attribute>
         </t>

    </t>
</templates>
```

Es posible que no se registren los cambios para ello hay que cargarlo desde un js

```Javascript
odoo.define("website_pnt.load", function (require) {
    "use strict";
    var ajax = require("web.ajax");
    var core = require("web.core");
    var QWeb = core.qweb;
    var load_xml = ajax.loadXML(
        "/website_pnt/static/src/xml/website_sale_stock_product_availability_pnt.xml",
        QWeb
    );
});
```