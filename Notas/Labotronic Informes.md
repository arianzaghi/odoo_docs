> [[060 - Clientes e Historias]]

Tags: 
Status: 
Related: 

___
# Labotronic

**Leyenda**
☑️: Cambios aceptados anteriormente/incidencia
✅: Cambios implementados
⌛: Peticiones nuevas o cambios no mencionados anteriormente (pertenecen a una historia nueva con modificaciones adicionales)
# Informes
## PV
- [ ] ☑️Quitar codigo antes de descripcion ✅
- [ ] ☑️Quitar datos bancarios ✅
- [ ] ☑️Poner condiciones y modos de pago ✅
- [ ] ⌛Quitar comercial de cabecera ✅
- [ ] ⌛Los precios son a dos decimales
![[Pasted image 20250612095833.png]]
### Factura Pro Forma
- [ ] ⌛ Modificar "Numero de factura proforma" a "Factura proforma"
- [ ] ⌛Poner condiciones y modos de pago
## Factura
**Titulos tabla**
- [ ] ☑️precio unitario > precio ud. ✅
- [ ] ☑️Cantidad -> CANT ✅
- [ ] ☑️disc% -> desc.% ✅
****
**Contenido informe**
- [ ] ☑️Poner modo y plazo de pago + cuenta bancaria ✅
- [ ] ☑️Quitar datos entidad bancaria ✅
- [ ] ⌛Los precios son a dos decimales✅
- [ ] ⌛ Quitar campo origen encabezado ✅
- [ ] ⌛Modificar columna producto 
- productoooooo  
	· HS   
	· NS AU9DAC cantidad 3  
	· NS AU9DAC cantidad 54
![[Pasted image 20250612095909.png]]

****
**Modificaciones modulo grouped by picking**
- [ ] ⌛ que solo salga referencia de albaran, no quieren que aparezca el pedido del que viene (en las lineas, encima del producto)
- [ ] ⌛ tampoco mostrar la fecha de ese albaran
- [ ] ⌛ la referencia del encabezado que salga junto a la linea del albaran (si juntan varios albaranes cada albaran puede tener una referencia)
- [ ] ⌛ Si no hay referencia en el producto que no aparezca el campo, en este caos no hay referencia y muestra el texto sin referencia:
![[Pasted image 20250612102943.png]]
## Albaran
- [ ] ☑️Ocultar descuento si no hay  ✅
- [ ] ⌛Que no aparezca la hora en fecha envio ✅
- [ ] ⌛Quitar columna impuestos ✅
- [ ] ⌛Formato albaran sin valorar ya no sale 
	- (Seria un formato del partner anterior)
- [ ] ⌛Los precios son a dos decimales ✅
- [ ] ⌛Modificar columna producto 
- producto
	· HS   
	· NS AU9DAC cantidad 3  
	· NS AU9DAC cantidad 54
****
- [ ] ☑️Renombrar columnas ✅
![[Pasted image 20250612093101.png]]

### Albarán Devolución
- [ ] ☑️la dirección aparece **dirección proveedor** y dejar solo **dirección** porque no es dirección de proveedor ✅
- [ ] ☑️ Quitar los plazos y modos de pago ✅
- [ ] ⌛ Al imprimir: que aparezca en el nombre **Albarán devolución + WH/Ret**,
- [ ] ⌛Quitar campo Peso de cabecera
- [ ] ⌛ Quitar horas de las fechas

![[Pasted image 20250612102445.png]]
****
**Albaran devolucion de compras**
- [ ] ⌛Quitar el campo pedido origen
![[Pasted image 20250612104823.png]]
## Reparaciones
**Confirmadas**
- [ ] ☑️Añadir formas de pago ✅:
- [ ] ⌛ Cuando en reparaciones es prespuesto, que el texto que sale en fecha de reparacion sea solo fecha porque aun no se ha reparado. y faltan las formas de pago.
	- **Confirmado**: Fecha reparacion
	- **Sin co​nfirmar**: Fecha
![[Pasted image 20250612104539.png]]
- [ ] ⌛ En la reparacion confirmada 25-0730 aparece un añadir, esto viene del tipo, quitar el tipo

| ![[Pasted image 20250612104359.png]] | ![[Pasted image 20250612104418.png]] |
| ------------------------------------ | ------------------------------------ |
****
**Presupuesto**
- [ ] ⌛ Presupuesto 25/0214. Modificar el texto inferior. Tiene que aparecer esto: ✅:
	- `Todos los presupuestos de reparación son estimativos, las cantidades o repuestos pueden variar. Estas variaciones se comunicarán previo presupuesto. En caso de no aceptación, LABOTRONIC,S.L. se reserva el derecho a facturar 1/2h de trabajo en concepto de emisión de diagnóstico.`
![[Pasted image 20250612104506.png]]
## Compras
**Presupuestos**
- [ ] ⌛PC 25-0730, quitar columna fecha prevista
- [ ] ⌛ poner un campo en la cabecera con la fecha del presupuesto
![[Pasted image 20250612103826.png]]
****
**Pedidos**
- [ ] ☑️Pedidos de compra se duplica el campo referencia de proveedor cuando está rellenado: Dejar solo uno ✅:
- [ ] ☑️Añadir formas de pago ✅:
- [ ] ⌛Quitar la columna fecha requerida
![[Pasted image 20250612104014.png]]

## Codigo HS
- [ ] ⌛resulta que no saben por qué están cambiados los nombres, y tiene que salir en los formatos el codigo que tiene 8 digitos que en el producto se llama codigo HS pero en esta lista se llama codigo local

| ![[Pasted image 20250612104918.png]] | ![[Pasted image 20250612104930.png]] |
| ------------------------------------ | ------------------------------------ |

