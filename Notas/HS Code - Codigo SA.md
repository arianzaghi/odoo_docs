> [[Añadir datos a informe]]

Tags: 
Status: 
Related: 

___

# HS Code - Codigo SA

> [!IMPORTANT]
> Localizado en `product.product`

## Desde `stock.move`
```xml
<td name="td_ml_hs_code" class="text-center">
    <t t-if="move.product_id.hs_code">
        <span t-field="move.product_id.hs_code"/>
    </t>
    <t t-else="">
        <span>&nbsp;</span>
    </t>
</td>
```

## Desde `stock.move.line`
```xml
<td name="td_sml_hs_code" class="text-center">
    <t t-if="move_line.product_id.hs_code">
        <span t-field="move_line.product_id.hs_code"/>
    </t>
    <t t-else="">
        <span>&nbsp;</span>
    </t>
</td>
```

