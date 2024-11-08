> [[Añadir datos a informe]]

Tags: 
Status: 
Related: 

___

# Incoterm

> [!IMPORTANT]
> Localizado en `sale.order`

## Desde `sale.order`
```xml
<div t-if="o.incoterm" class="col-auto" name="div_incoterm">
	<strong>Incoterm:</strong>
	<p t-field="o.incoterm"/>
</div>
```

## Desde `stock.picking`
```xml
<div t-if="o.sale_id.incoterm" class="col-auto" name="div_incoterm">
	<strong>Incoterm:</strong>
	<p t-field="o.sale_id.incoterm"/>
</div>
```

