> [[Workflow Punt]]

Tags: 
Status: 
Related: 

___

# Instalar módulos en odoo

## Requisitos

- Nombre del repositorio 
	`stock-logistics-warehouse`
- Nombre del modulo
	`stock_mts_mto_rule`
- Link del repo (opcional)
	` https://github.com/OCA/stock-logistics-warehouse/tree/17.0/stock_mts_mto_rule`

## Instalación

1. Navegamos a la carpeta `oca` del cliente
	`odoo170/src/addons-custom/cliente/oca`

2. Ejecutamos la siguiente instrucción
	`ln -sf ../../REPOSITORIO/MODULO .`

3. Lanzamos client_mirror
	`./git_client_mirror.sh cliente.txt`

> [!IMPORTANT] Importante
> La ruta que estamos poniendo en el paso 2 NO existe en local (no se auto completará mientras la escribimos). Esa ruta existe dentro del servidor.

> En el paso 2 creamos un acceso directo que no existe en nuestro equipo local. Tras la ejecución de `git_client_mirror`, se instala en nuestro equipo el módulo


> [!DANGER] Recuerda
> Después de instalar el módulo hay que activarlo, tanto en el docker de pruebas como en PRO


## Adicionalmente

1. Comprobamos que en nuestro local en `/opt/sources/odoo170/src/` exista el modulo que estamos instalando (`bank_payment`), y que este actualizado (`git pull`)
2. Creamos enlace en el servidor, git log y git mirror en nuestro local
3. añadir linea en nuestro config


Primero se debe crear el link en la carpeta OCA. En OCA hay un readme donde te dice exactamente el comando a utilizar. Solo debes cambiar el nombre por el nombre del módulo a instalar.

Luego de creado el link, te armas el docker y dentro del docker te instalas el módulo. Tienes que darle a actualizar aplicaciones.

Si no te aparece en la listas de aplicaciones, debes entrar al servidor del cliente, entras a odoo, src y ahí buscas la carpeta del módulo y le haces git pull. El git pull lo debes hacer en la carpeta del MODULO (por ejemplo stock) que contiene a los modelos (stock.picking, etc). Y ese git pull te actualiza el módulo completo, sería el modelo que necesitas y el que no necesitas también. Luego de hacer esto en el servidor, debes reabrir la pull requests (reopen).

Con esto hay que tener cuidado porque si no hace un update_all durante mucho tiempo, tendrás el módulo instalado súper actualizado y el resto de src muy atrasado.

Para pasar el módulo a tu local, debes subir el docker a producción y hacerte el client_mirror en tu local. Y así tendrías el módulo nuevo en tu local.