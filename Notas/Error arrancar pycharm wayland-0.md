> [[Errores]]

Tags: 
Status: 
Related: 

___
# wayland

> Al abrir el `pycharm`, nos sale el siguiente error

```sh
Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: error mounting "/run/user/1000/gdm/Xauthority" to rootfs at "/tmp/.wayland_docker/xauthority": create mount destination for /tmp/.wayland_docker/xauthority mount: create target of file bind-mount: mknod regular file /home/docker/overlay2/06b77e0e8ecbcbe242c3188efc55bff763f221a5ccaa8ac8f8c6067ab23a78f6/merged/tmp/.wayland_docker/xauthority: read-only file system: unknown
```

**Solución**
1. Configuramos la variable de entorno
	`WAYLAND_DISPLAY='wayland-0'`
2. Exportamos la variable
	`export WAYLAND_DISPLAY`
3. Eliminamos el docker
	`docker rm pycharm-odooo-17`
4. Volvemos a arrancar el docker
	`pycharm_odoo 17`

> [!INFO] env
> > Si escribimos `env` en la terminal, deben de salir las variables del entorno. Comprobamos que esté `wayland-0`.

> [!INFO] x11 vs gnome
> > Si no nos funciona, podemos intentar a cambiar el entorno gráfico de `Ubuntu` a `x11` deslogueándonos y cambiando el entorno abajo del todo a la derecha en la ruedecita, cuando vamos a iniciar sesión en Ubuntu con nuestro usuario.

