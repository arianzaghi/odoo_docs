> [[Modificaciones comunes XLM]]

Tags: 
Status: 
Related: 

___

# Alinear contenido columna a la derecha

## V16

```xml
<t t-if="label.product_packaging_id">
    <td class="text-right">
        <t t-esc="my_model.get_packages_qty()"/>
    </td>
</t>
```

```xml
    <td class="text-right">
```

## V17

```xml
<t t-if="label.product_packaging_id">
    <td class="text-end">>
        <t t-esc="my_model.get_packages_qty()"/>
    </td>
</t>
```

```xml
    <td class="text-end">
```
