> [[Odoo Views Vistas]]

Tags: 
Status: 
Related: 

___

# Importar hoja de estilos en xml

Queremos establecer en un fichero xml una serie de estilos para utiilizarlos en el resto de formatos.

**Fichero de estilos**
```xml
<?xml version="1.0" encoding="utf-8"?>  
<odoo>  
	<template id="custom_styles">  
		<link href="[https://fonts.googleapis.com/css2?family=Manrope:wght@200..800"](https://fonts.googleapis.com/css2?family=Manrope:wght@200..800%22 "https://fonts.googleapis.com/css2?family=manrope:wght@200..800%22")  
		              rel="stylesheet"/>  
		<style>  
			.titulo {font-family:'Manrope'; font-size:14pt;}  
			.subtitulo {font-family:'Arial'; font-size:12pt;}  
			.watermark {  
				position: fixed;  
				top: 15%;  
				right: -5%;  
				opacity: 0.5;  
				z-index: -1;  
				transform: rotate(-45deg);  
				transform: translateY(-50px);  
			}  
		</style>  
	</template>  
</odoo>
```

**Importamos el fichero de estilos**
```xml
<div t-attf-class="article o_report_layout_standard o_company_#{company.id}_layout" t-att-data-oe-model="o and o._name" t-att-data-oe-id="o and o.id" t-att-data-oe-lang="o and o.env.context.get('lang')">
	<div class="pt-5">

		<!-- AQUI INVOCAMOS NUESTROS ESTILOS -->
		<t t-call="report_pnt.custom_styles"/> 
		
		<!-- Aqui invocamos el contenido del informe -->
		<t t-call="web.address_layout"/>
		
		<div class="watermark">
			<img src="report_pnt/static/img/pnt_marca_agua.png" alt="Watermark" style="max-width: 830px; height: auto; margin-top: 70%; margin-bottom: -120px"/>
		</div>
	</div>
	<t t-raw="0"/>
</div>
```

Los informes que invocamos desde el layout template, también tendrán acceso a los estilos declarados.

## Ejemplos
### 1. Punt
[Punt_49238](https://github.com/puntsistemes/punt-sistemes_odoo/commit/c32cd80f47bde94f251eef3831e493c1349ff1df#diff-881fc2325f35f67d56d200b8d8290abcad4ebea944eb5fccd112756ce01d51e5L150-L155)