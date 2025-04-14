> [[032 - Tipos de Vistas]]

Tags: 
Status: 
Related: 

___
# Vista Pivot
![[Pasted image 20241218090614.png]] ^88f40e

1. **Medidas:** Son datos NO agrupables (`int`, `float,` `char`...) Es el dato que queremos visualizar
2. **Columnas:** Utilizamos datos por los que sí se puede agrupar (`Many2one`, `Date`, `Selection`...) No se puede usar `One2many`
3. **Filas:** Igual que las columnas.

> [!WARNING] El orden de los campos en la vista importa
> Según el orden en que pongamos los campos en `xml`, veremos la vista pivot por default.
> Utilizaremos:
> 
> 	1. Medidas
> 	2. Columnas
> 	3. Filas

![[Pasted image 20241127163851.png]]

### [[Añadir vista pivot]]
### [[Añadir campo vista pivot]]

### [[Informe SQL Para vista pivot o tree (como sale_report)]] (mejor que modelo intermedio)
### [[Modelo intermedio para ver medidas como filas en pivot]]
