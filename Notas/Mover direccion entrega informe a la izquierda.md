> [[Mover o modificar elementos de informe]]

Tags: 
Status: 
Related: 

___

# Mover direccion entrega informe a la izquierda

## ALBARAN

> En el albarán nos piden dejar solo la direccion de entrega y ponerla a la izquierda

```xml
<!--        Ocultar direccion facturacion y entrega-->  
<xpath expr="//t[@t-set='information_block']" position="attributes">  
    <attribute name="t-if" add="False" separator=" and "/>  
</xpath>  
  
<!--        Ocultar direccion entrega-->  
<xpath expr="//t[@t-set='address']" position="attributes">  
    <attribute name="t-if" add="False" separator=" and "/>  
</xpath>  
  
<!--        Direccion entrega-->  
<xpath expr="//t[@t-set='partner']" position="after">  
    <div class="row">  
        <div class="col-6">  
            <div name="div_out_address">  
                <div name="out_delivery_address"  
                     t-if="o.should_print_delivery_address()">  
                    <span>  
                        <strong>Delivery Address:</strong>  
                    </span>  
                    <div t-field="o.move_ids[0].partner_id"  
                         t-options='{"widget": "contact", "fields": ["address", "name", "phone", "vat"], "no_marker": True, "phone_icons": True}'/>  
                </div>  
                <div name="out_warehouse_address"  
                     t-elif="o.picking_type_id.code != 'internal' and o.picking_type_id.warehouse_id.partner_id">  
                    <span>  
                        <strong>Warehouse Address:</strong>  
                    </span>  
                    <div t-field="o.picking_type_id.warehouse_id.partner_id"  
                         t-options='{"widget": "contact", "fields": ["address", "name", "phone", "vat"], "no_marker": True, "phone_icons": True}'/>  
                </div>  
            </div>  
        </div>  
    </div>  
</xpath>
```

## PEDIDO VENTA

```xml
<!--        Ocultar direccion facturacion -->  
<xpath expr="//t[@t-set='information_block']" position="attributes">  
    <attribute name="t-if" add="False" separator=" and "/>  
</xpath>  
  
<!--        Ocultar direccion entrega-->  
<xpath expr="//t[@t-set='address']" position="attributes">  
    <attribute name="t-if" add="False" separator=" and "/>  
</xpath>


```