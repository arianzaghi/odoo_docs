> [[Errores]]

Tags: 
Status: 
Related: 

___

# Error deployment Github Actions

> **Problema:** Falta una librería en el docker de pruebas y no se puede hacer el deployment

## Solución

**Modificamos `docker.sh` en la raíz de la rama main (16.0) y descomentamos lo siguiente**
```sh
# pip
 packages=('{{pyotp}}') # AÑADIR AQUI LIBRERIAS PIP
 installed_packages=$(pip freeze)
 install=()
 for package in "${packages[@]}"; do
   if ! echo "${installed_packages}" | grep -iq "^${package}==\|^${package}"; then
     install+=("${package}")
   fi
 done
 if [[ ${#install[@]} -gt 0 ]]; then
   pip install --no-cache-dir "${install[@]}"
 fi
```


> [!Information] Detalles
> - Añadimos los paquetes/librerias que hagan falta instalar en pip
> - Commiteamos directamente en `main` y actualizamos la PR del docker (`update branch`)
