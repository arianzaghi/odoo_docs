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

## **Selección de versiones**
```bash
# Variables editables ↓↓↓
# Para añadir versiones nuevas al equipo, ir al final del script y comentar la parte indicada
VERSIONS_ODOO=(17.0 16.0 15.0 14.0 13.0 12.0 11.0 10.0 9.0 8.0) # Versiones de Odoo a descargar
# Variables editables ↑↑↑
```

## Instalación dependencias (solo primera ejecuci)
```bash
# Comentar para cargar nuevas versiones ↓↓↓
# Asegúrese antes de tener actualizado el repositorio dev-tools
download_dev_repository
configure_enviroment_pycharm
install_packages
install_postgres_client
disable_postgresql
install_docker
download_pycharm
install_cron
UPDATE=1
# Comentar para cargar nuevas versiones ↑↑↑
```