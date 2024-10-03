> [[Albaran (ALB)]]

Tags: 
Status: 
Related: 

___

# Direcciones de entrega albaran

> Las direcciones de entrega y envió se almacenana en dos variables
> mediante un `<t t-set>` y después la estructura del informe los invoca para que se muestren


## Direcciones en `report_delivery_document` CORE
```xml
%% Bloque de direcciones para caso A %%
<t t-set="address">  
    <div name="div_outgoing_address">  
        <div name="outgoing_delivery_address" t-if="o.should_print_delivery_address()">  
            <span><strong>Delivery Address:</strong></span>  
            <div t-field="o.move_ids[0].partner_id"  
                t-options='{"widget": "contact", "fields": ["address", "name", "phone"], "no_marker": True, "phone_icons": True}'/>  
        </div>  
        <div name="outgoing_warehouse_address"  
             t-elif="o.picking_type_id.code != 'internal' and o.picking_type_id.warehouse_id.partner_id">  
            <span><strong>Warehouse Address:</strong></span>  
            <div t-field="o.picking_type_id.warehouse_id.partner_id"  
                t-options='{"widget": "contact", "fields": ["address", "name", "phone"], "no_marker": True, "phone_icons": True}'/>  
        </div>  
    </div>

%% Bloque de direcciones para caso B %%
<t t-set="information_block">  
    <div class="row">  
        <div class="col-7" name="div_incoming_address">  
            <t t-set="show_partner" t-value="False" />  
            <div name="vendor_address" t-if="o.picking_type_id.code=='incoming' and partner">  
                <span><strong>Vendor Address:</strong></span>  
                <t t-set="show_partner" t-value="True" />  
            </div>  
            <div name="customer_address" t-if="o.picking_type_id.code=='outgoing' and partner and partner != partner.commercial_partner_id">  
                <span><strong>Customer Address:</strong></span>  
                <t t-set="show_partner" t-value="True" />  
            </div>  
            <div t-if="show_partner" name="partner_header">  
                <div t-field="partner.commercial_partner_id"  
                     t-options='{"widget": "contact", "fields": ["address", "name", "phone", "vat"], "no_marker": True, "phone_icons": True}'/>  
            </div>  
        </div>  
    </div>  
</t>
</t>
```

## Modificar direcciones
> Podemos ocultar esos dos t-sets y volverlos a definir como nosotros queramos

### `re-definir bloques`
```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <template id="pnt_report_delivery_return_document" inherit_id="stock.report_delivery_document">

        <!-- Hide the original address blocks if it's a return -->
        <xpath expr="//div[@name='div_outgoing_address']" position="attributes">
            <attribute name="t-if">not o.picking_type_id.pnt_return_report</attribute>
        </xpath>

        <xpath expr="//div[@name='div_incoming_address']" position="attributes">
            <attribute name="t-if">not o.picking_type_id.pnt_return_report</attribute>
        </xpath>

        <!-- Add new blocks for swapped addresses if it's a return -->
        <xpath expr="//t[@t-set='information_block']" position="after">
            <t t-if="o.picking_type_id.pnt_return_report">
                <!-- Swapped block for the outgoing address -->
                <t t-set="information_block">
                    <div name="div_outgoing_address">
                        <div name="outgoing_warehouse_address" style="border: solid 1px green"
                             t-if="o.picking_type_id.code != 'internal' and o.picking_type_id.warehouse_id.partner_id">
                            <span>
                                <strong>2xWarehouse Address:</strong>
                            </span>
                            <div t-field="o.picking_type_id.warehouse_id.partner_id"
                                 t-options='{"widget": "contact", "fields": ["address", "name", "phone"], "no_marker": True, "phone_icons": True}'/>
                        </div>

                        <div name="outgoing_delivery_address" style="border: solid 1px red"
                             t-if="o.should_print_delivery_address()">
                            <span>
                                <strong>2xDelivery Address:</strong>
                            </span>
                            <div t-field="o.move_ids[0].partner_id"
                                 t-options='{"widget": "contact", "fields": ["address", "name", "phone"], "no_marker": True, "phone_icons": True}'/>
                        </div>
                    </div>
                </t>

                <!-- Swapped block for the incoming address -->
                <t t-set="address">
                    <div class="row">
                        <div class="col-7">
                            <div name="vendor_address"
                                 t-if="o.picking_type_id.code=='outgoing' and partner and partner != partner.commercial_partner_id">
                                <span>
                                    <strong>1xCustomer Address:</strong>
                                </span>
                                <div t-field="partner.commercial_partner_id"
                                     t-options='{"widget": "contact", "fields": ["address", "name", "phone", "vat"], "no_marker": True, "phone_icons": True}'/>
                            </div>

                            <div name="customer_address" t-if="o.picking_type_id.code=='incoming' and partner">
                                <span>
                                    <strong>1xVendor Address:</strong>
                                </span>
                                <div t-field="partner.commercial_partner_id"
                                     t-options='{"widget": "contact", "fields": ["address", "name", "phone", "vat"], "no_marker": True, "phone_icons": True}'/>
                            </div>
                        </div>
                    </div>
                </t>
            </t>
        </xpath>
```