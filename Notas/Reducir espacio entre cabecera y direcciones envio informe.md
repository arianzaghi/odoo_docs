> [[Mover o modificar elementos de informe]]

Tags: #informe 
Status: 
Related: 

___

# Reducir espacio entre cabecera y direcciones envio informe

> Cuando te piden subir la información del formato sin tocar el papel format para que solo afecte a ese informe se puede hacer así:
> Heredas el page y le das al style negativo y en vez de agrandar el margen te lo achica.

| ![[Pasted image 20240808115353.png]] | ![[Pasted image 20240808115348.png]] |
| ------------------------------------ | ------------------------------------ |
```xml
<xpath expr="//div[hasclass('page')]" position="attributes">
	<attribute name="style">margin-top:-90px!important;</attribute>
</xpath>
```