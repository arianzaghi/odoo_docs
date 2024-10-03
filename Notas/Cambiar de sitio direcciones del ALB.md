> [[Albaran (ALB)]]

Tags: 
Status: 
Related: 

___

# Cambiar de sitio direcciones del ALB

1. [[Comprobar si es ALB de devolucion]]
2. Ocultar los campos originales
3. Volver a definir los campos de devolución

```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
    <template id="pnt_report_delivery_return_document" inherit_id="stock.report_delivery_document">  
    
        # OCULTAMOS LOS ADDRESS ANTIGUOS
    
		<t  t-set="address" position="attributes">  
             <attribute name="t-if">not o.picking_type_id.pnt_is_return_type</attribute>  
        </t>  
        <t t-set="information_block" position="attributes">  
             <attribute name="t-if">not o.picking_type_id.pnt_is_return_type</attribute>  
        </t>

		# PONEOS LOS ADDRESS NUEVOS

        <div class="page" position="before">  
            <div t-if="o.picking_type_id.pnt_is_return_type">  
                <div class="row">  
                    <div class="col-7">  
                        <div name="outgoing_delivery_address"  
                             t-if="o.should_print_delivery_address()">  
                            <span>  
                                <strong>Delivery Address:</strong>  
                            </span>  
                            <div t-field="o.move_ids[0].partner_id"  
                                 t-options='{"widget": "contact", "fields": ["address", "name", "phone"], "no_marker": True, "phone_icons": True}'/>  
                        </div>  
                        <div name="outgoing_warehouse_address"  
                             t-elif="o.picking_type_id.code != 'internal' and o.picking_type_id.warehouse_id.partner_id">  
                            <span>  
                                <strong>Warehouse Address:</strong>  
                            </span>  
                            <div t-field="o.picking_type_id.warehouse_id.partner_id"  
                                 t-options='{"widget": "contact", "fields": ["address", "name", "phone"], "no_marker": True, "phone_icons": True}'/>  
                        </div>  
                    </div>  
                    <div class="col-5">  
                        <div name="div_incoming_address">  
                            <t t-set="show_partner" t-value="False"/>  
                            <div name="vendor_address" t-if="o.picking_type_id.code=='incoming' and partner">  
                                <span>  
                                    <strong>Address:</strong>  
                                </span>  
                                <t t-set="show_partner" t-value="True"/>  
                            </div>  
                            <div name="customer_address"  
                                 t-if="o.picking_type_id.code=='outgoing' and partner and partner != partner.commercial_partner_id">  
                                <span>  
                                    <strong>Address:</strong>  
                                </span>  
                                <t t-set="show_partner" t-value="True"/>  
                            </div>  
                            <div t-if="show_partner" name="partner_header">  
                                <div t-field="partner.commercial_partner_id"  
                                     t-options='{"widget": "contact", "fields": ["address", "name", ], "no_marker": True, "phone_icons": True}'/>  
                                <br/>  
                                <br/>  
                                <br/>  
                                <span t-field="partner.commercial_partner_id.phone"/>  
                                <span t-field="partner.commercial_partner_id.vat"/>  
                            </div>  
                        </div>  
                    </div>  
                </div>  
            </div>  
        </div>
```