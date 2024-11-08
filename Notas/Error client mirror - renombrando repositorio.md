> [[git_client_mirror.sh]]

Tags: 
Status: 
Related: 

___

# Error client mirror - renombrando repositorio

> Estamos hacinedo el `client mirror` de un cliente, pero nos salta el siguiente error antes de terminar
> ![[Pasted image 20241107090604.png]]
## Solución

1. Renombramos `core_20241107074901` a `core`
	1. `mv core_20241107074901 core`
2. Entramos en `core` y hacemos un fetch
	1. `git fetch origin 17.0`
3. Volvemos a lanzar el `client_mirror`