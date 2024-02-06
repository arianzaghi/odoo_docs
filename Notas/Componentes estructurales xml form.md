> [[Vista Form - Formulario]]

Tags: 
Status: 
Related: 

___

# Componentes estructurales xml form

### notebook
Define una sección con pestañas. Cada pestaña se define como una `page` nueva.

### group
Se usa para definir columnas en el layout del formulario. Por defecto group define 2 columnas.
El numero de columnas en un grupo se puede personalizar usando el atributo `col`.
El número de columnas que ocupa un elemento se puede personalizar usando `colspan`.

### newline
Se utiliza dentro de elementos `group` para saltar a la linea siguiente (sin rellenar las columnas restantes)
only useful within `group` elements, ends the current row early and immediately switches to a new row (without filling any remaining column beforehand)

### separator
Espaciado horizontal con atributo `string` que se comporta como un título se sección.

### sheet

can be used as a direct child to `form` for a narrower and more responsive form layout

### header

combined with `sheet`, provides a full-width location above the sheet itself, generally used to display workflow buttons and status widgets

