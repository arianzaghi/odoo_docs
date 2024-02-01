> [[BBDD|Back]]

Tags: 
Status: 
Related: 

___

# Cambiar la bbdd que se usa en el docker

Modificamos `github_repo_cliente > github_actions.config > ODOO_DB_DOCKER y ODOO_DB_DOCKER_PORT`

```python
ACTIONS_GIT_PATH='/opt/odoo/github_actions'  

# -- MODIFICAR -- #
ODOO_DB_DOCKER='SIGNES'  
ODOO_DB_DOCKER_PORT=5432
# -- MODIFICAR -- #

ODOO_PRO_DB='SIGNES'  
ODOO_PRO_DB_PORT=5432  
ODOO_PRO_PATH_ADDONS_CUSTOM='/opt/odoo/odoo120/src/addons-custom'  
ODOO_PRO_PATH_ATTACHMENTS='/opt/odoo/odoo120/attachments'  
ODOO_PRO_PATH_CONFIG='/opt/odoo/odoo120/conf/odoo120.conf'  
ODOO_PRO_PATH_ODOO_BIN='/opt/odoo/odoo120/src/core/odoo-bin'  
ODOO_PRO_PATH_PYTHON='/opt/odoo/odoo120/virtualenv/bin/python3.5'  
ODOO_PRO_PATH_SRC='/opt/odoo/odoo120/src'  
ODOO_PRO_SERVICE='odoo120'  
ODOO_PRO_VERSION=12  
ODOO_STA_DB='DEV'  
ODOO_STA_DB_PORT=5433  
ODOO_STA_PATH_ADDONS_CUSTOM='/opt/odoo/odoo120dev/src/addons-custom'  
ODOO_STA_PATH_ATTACHMENTS='/opt/odoo/odoo120dev/attachments'  
ODOO_STA_PATH_CONFIG='/opt/odoo/odoo120dev/conf/odoo120dev.conf'  
ODOO_STA_PATH_ODOO_BIN='/opt/odoo/odoo120dev/src/core/odoo-bin'  
ODOO_STA_PATH_PYTHON='/opt/odoo/odoo120dev/virtualenv/bin/python3.5'  
ODOO_STA_PATH_SRC='/opt/odoo/odoo120dev/src'  
ODOO_STA_SERVICE='odoo120dev'  
ODOO_STA_VERSION=12
```