> [[Bash y scripts]]

Tags: 
Status: 
Related: 

___

# install_development.sh

Script principal para instalar las diferentes versiones de odoo en local.

> [!EJECUTAR SCRIPT]
> `chmod +x install_development.sh` --> (si no tenemos permisos)
> `./install_development.sh`

## Añadir nuevas versiones de odoo
Caso en que ya tenemos la instalación hecha y solamente queremos añadir una nueva versión de odoo

### 1.  Indicamos las versiones que queremos

```python
#!/bin/bash
set -eu
clear

# Variables personalizables, pueden ser editadas
VERSIONS_ODOO=(16.0 15.0 14.0 13.0 12.0 11.0 10.0 9.0 8.0) # Versiones de Odoo a descargar
# Variables personalizables, pueden ser editadas

# ----- RESTO DEL SCRIPT ------ #
```

### 2. Comentamos instalaciones innecesarias
Comentamos el penúltimo bloque de instalaciones 

```python
# ----- Comentar para descargar nuevas versiones ↓↓↓
#install_packages
#configure_enviroment_pycharm
#install_docker
#install_postgres_client
#download_pycharm
# ----- Comentar para descargar nuevas versiones ↑↑↑

# No comentar ↓↓↓
download_sources_odoo
unset DEBIAN_FRONTEND
unset USER_PASS_SUDO
echo
echo "Instalación finalizada correctamente."
echo
echo "Reinicie antes para que funcione PyCharm y docker."
# No comentar ↑↑↑

# ----- FINAL DEL SCRIPT ----- #
```