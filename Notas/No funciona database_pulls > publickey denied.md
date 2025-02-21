> [[Clonar o descargar la bbdd del docker de github]]

Tags: 
Status: 
Related: 

___

# No funciona database_pulls

> Al intentar descargar la bbdd de un docker, nos salta el error `public key denied`

**Solución:**

Ejecutamos en la carpeta `~/.ssh`:
```sh
ln -sf ../sources/dev-tools/ssh_keys/github_actions_dockers .
ln -sf ../sources/dev-tools/ssh_keys/github_actions_dockers.pub .
```