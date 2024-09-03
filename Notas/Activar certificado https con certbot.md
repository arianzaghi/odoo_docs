> [[Back]]

Tags: 
Status: 
Related: 

___

# Activar certificado https con certbot

1. Lanzamos `certbot` como sudo para activar el HTTPS.

- Nos preguntará que dominio queremos activar
- Repetimos el proceso para cada dominio


![[Pasted image 20240507170753.png]]

2. Añadimos `http2` en los ficheros de configuración

- Después de lanzar `certbot` volvemos a abrir los ficheros
- Vemos que abajo del todo salen nuevas líneas de configuración
- Añadimos `http2` en las zonas marcadas a continuación
- Repetir para ambos ficheros

![[Pasted image 20240507171537.png]]