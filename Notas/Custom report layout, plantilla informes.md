> [[Informes XML]]

Tags: 
Status: 
Related: 

___

# Custom report layout, plantilla informes

> Con esta plantilla, definimos un layout para nuestros informes. Tenemos los siguientes templates:
> - Cabecera
> - Footer
> - Cuerpo del documento.

Seleccionamos este layout desde configuración

```xml
<template id="report_layout_footer_pnt">  
    <div class="text-start" style="page-break-inside: avoid; border: solid 1px red;">  
        <div t-if="o and o._name in ['account.move']" name="first_row" style="font-size: 10pt;"  
             class="text-justify">  
            <div>  
                OUR BANK DATA FOR TRANSFER PAYMENT  
            </div>  
            <div class="row">  
                <div class="col-12">  
                    <strong>ENTITY:</strong>  
                    <span t-esc="o.company_id.get_bank_info()"/>  
                    <strong t-translation="off">IBAN:</strong>  
                    <span t-esc="o.company_id.get_bank_iban()"/>  
                    <strong>-</strong>  
                    <strong>SWIFT/CODE:</strong>  
                    <span t-esc="o.company_id.get_bank_swift()"/>  
                </div>  
            </div>  
        </div>  
        <br/>  
        <div name="data_protection_info_long" style="text-align: left; page-break-inside: avoid; font-size: 8pt"  
             class="text-justify col-12">  
            <span t-field="company.report_footer"/>  
        </div>  
        <div name="third_row" style="font-size: 10pt;" class="row">  
            <div class="col-1">  
                <div t-if="report_type == 'pdf'">  
                    <br/>  
                    <span class="page"/>  
                    /  
                    <span class="topage"/>  
                </div>  
            </div>  
        </div>  
    </div>  
</template>  
  
<template id="report_layout_header_pnt">  
    <div class="row">  
        <div class="col-6">  
            <img t-if="o.company_id.logo" t-att-src="image_data_uri(o.company_id.logo)" alt="Logo" style="margin-top: 9%"/>  
        </div>  
        <div class="col-6">  
            <div class="company_address" style="text-align: right; margin-left: auto">  
                <span t-field="o.company_id.company_details"/>  
                <div class="clearfix mb8"/>  
            </div>  
        </div>  
    </div>  
    <div name="header_separator">  
        <label string="  "  
               t-attf-style="display:block; border-top:2px solid grey; margin-top: 20px;"/>  
    </div>  
</template>  
  
<template id="external_layout_pnt">  
    <div t-attf-class="header o_company_#{company.id}_layout" t-att-style="report_header_style">  
        <div class="row">  
            <div class="col-12">  
                <t t-if="o" t-call="report_pnt.report_layout_header_pnt"/>  
            </div>  
        </div>  
        <div name="header_separator">  
            <label string="  "  
                   t-attf-style="display:block; border-top:2px; margin-top: 20px;"/>  
        </div>  
    </div>  
  
    <div t-attf-class="article o_report_layout_standard o_company_#{company.id}_layout"  
         t-att-data-oe-model="o and o._name" t-att-data-oe-id="o and o.id"  
         t-att-data-oe-lang="o and o.env.context.get('lang')">  
        <div class="pt-5">  
            <t t-call="web.address_layout"/>  
        </div>  
        <t t-raw="0"/>  
    </div>  
  
    <div t-attf-class="footer o_standard_footer o_company_#{company.id}_layout">  
        <t t-call="report_pnt.report_layout_footer_pnt"/>  
    </div>  
</template>  
  
<record id="report_layout_pnt" model="report.layout">  
    <field name="name">Pnt Layout</field>  
    <field name="sequence">10</field>  
    <field name="view_id" ref="report_pnt.external_layout_pnt"/>  
</record>
```