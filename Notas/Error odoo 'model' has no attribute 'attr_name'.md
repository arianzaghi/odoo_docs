> [[Back]]

Tags: 
Status: 
Related: 

___

# Error odoo 'model' has no attribute 'attr_name'

![[Pasted image 20240417165228.png]]

Te cuento un poco sobre el error que nos daba la vista de Zubi. Te acuerdas que no sabíamos porque se generaba ese error si no estaba en Pycharm? Bueno resulta que ellos tocan Odoo, entonces han creado un campo dentro de Odoo que se llama new_footer. Solo te aparece en Vistas y Campos dentro de Ajustes dentro de Odoo. Te aviso para que lo sepas jaja

Le expliqué a Isaac como funcionaba el código, y automáticamente me dijo que eso pasa cuando alguien toca Odoo. Y me dijo que vaya a vistas y a campos a comprobarlo. Y PUM! Ahí estaba

Y hay dos formas de solucionarlo:

1) Definis el campo y listo. Es la opción "simple".

2) Pones el módulo de ellos como dependencia del report o del custom según estés trabajando vos y listo. Con eso apañado