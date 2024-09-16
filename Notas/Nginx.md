1) Para poder modificar un nginx tienes que entrar como sudo su dentro del servidor.
   
2) Nano para modificar o cat para leer
   nano /etc/nginx/sites-available/odoo.puntsistemes.com.conf
   En esta ruta encontramos el archivo nginx del servidor
   
3) Configuración anterior del Nginx
   
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeXRhLechcd38_oNPz-7o9X_wgVT04c5j2rPDaEHbIxNTQ_HaU5dEyYb4hfag8G7RVJ7kjGMm_bmVv-_V6jby-2jzu5c3omKXNiPaCnVfoE8FEAV2DxfDSUDKlLjjQfzHgcwXT3kIllxxL8b-WfUqJd-j8L?key=wRleysEJJnMZ9qGrW6z0iQ)

El objetivo de la historia era agregarle un nuevo dominio llamado "demo16.puntsistemes.com"

4) Entonces se realizaron los siguientes cambios:
   
![[Pasted image 20240916125821.png]]
 
 La modificación se hace en las primeras seis líneas luego del server{}
 
 Se agrega el nuevo dominio igual que lo solicitaron y se cambio al puerto 80 que es el puerto que lee el comando certbot.
 
 5) Luego de modificado se debe reiniciar el nginx con el comando de siempre "systemctl restart nginx".
    
6) Luego debes lanzar el comando "certbot" para darle el certificado al dominio y debes poner el número que corresponde al dominio que quieres autorizar.
   
7) Una vez que el dominio ya tiene el certificado, debes agregar el http2 en las líneas de listen del certificado. 
   
   ![[Pasted image 20240916130006.png]]
   
   8) Luego de agregar el http2 debes volver a lanzar "systemctl restart nginx". Y ya queda de categoría.