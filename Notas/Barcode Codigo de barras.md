> [[Reportes o Informes]]

Tags: 
Status: 
Related: 

___

# Barcode Codigo de barras

```xml
<div class="col-md-12" style="margin-top: 6%; text-align: center;">  
    <span 
	    t-if='label.product_id.barcode'
		t-out="label.product_id.barcode"
		class="barcode ms-2"
		t-options="{'widget': 'barcode', 'width': 200, 'height': 100, 'quiet': 0, 'humanreadable': 1}"
		style="display: inline-block;"
	/>  
</div>
```

```xml
<div t-field="ml.product_id.barcode" t-options="{'widget': 'barcode', 'symbology': 'auto', 'width': 400, 'height': 100, 'quiet': 0, 'img_style': 'height:35px;'}"/>
```