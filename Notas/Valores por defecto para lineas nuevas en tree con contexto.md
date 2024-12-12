> [[Contextos]]

Tags: 
Status: 
Related: 

___

# Valores por defecto para lineas nuevas en tree con contexto

> Queremos crear `room.bookings` desde un `crm.lead` y que coja por defecto como nombre, el nombre del `lead`

![[Pasted image 20241212125930.png]]

1. Utilizamos el `default_get` en el modelo destino para ver de donde se esta llamando

![[default get#^1cd9f9]]

2. Desde el `params` podemos ver el modelo y el id desde donde hemos creado la linea nueva
3. Añadimos al `res` los valores nuevos que necesitamos, y se cargaran por defecto