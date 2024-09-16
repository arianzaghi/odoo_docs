Tags: 
Status: 
Related: #servidor [[Instalar Odoo Servidor Cliente]]

___

# Error instalación con Domino DNS equivocado

> Si instalamos el servidor con un `dominio` que no funciona, tendremos el siguiente error:

![[Pasted image 20240507165702.png]]
- **Dominio Incorrecto:** `odoo.coelbe.com`
- **Dominio Correcto:** `coelbe.puntsistemes.cloud`

## Solución

1. Accedemos como root al servidor

- Ya podemos hacer ssh al domain nuevo (si está bien configurado)
```bash
ssh -i ~/.ssh/ssh_key_private -p 2228 odoo@coelbe.puntsistemes.cloud
```

2. Navegamos a `/etc/nginx/sites-enabled/`
![[Pasted image 20240507170001.png]]

3. Tenemos que modificar ambos ficheros (dev y pro) con los `dominios` correctos

| **Version Incorrecta**               | **Version Correcta**                 |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20240507170320.png]] | ![[Pasted image 20240507170606.png]] |





![[Pasted image 20240507163721.png]]
4. Lanzamos `certbot` para activar el HTTPS.

- Nos preguntará que dominio queremos activar
- Repetimos el proceso para cada dominio

![[Pasted image 20240507170753.png]]

5. Añadimos `http2` en los ficheros de configuración

- Después de lanzar `certbot` volvemos a abrir los ficheros
- Vemos que abajo del todo salen nuevas líneas de configuración
- Añadimos `http2` en las zonas marcadas a continuación
- Repetir para ambos ficheros

![[Pasted image 20240507171537.png]]

6. Reiniciamos `nginx` como `root`

```bash
systemctl restart nginx
```