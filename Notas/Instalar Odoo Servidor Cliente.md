> [[Server]]

Tags: 
Status: 
Related: [[Error instalación con Domino DNS equivocado]]

___

# Instalar v17

## Requisitos

- **IP Servidor**
- **Dominio PRO y DEV**
- **Versión de ODOO** 
- **Enterprise**

## Instalación

1. Comprobamos Dominio DNS
	`DNS Checker` https://dnschecker.org/
	Si el `dominio` no funciona, lo pedimos a sistemas. Sin `dominio` no podemos seguir

2.  Buscamos la passwords del servidor cliente
	`Odoo > Passwords > Ubuntu > Cliente`

3.  Nos conectamos al servidor nuevo (NO POR ALIAS)
```bash
ssh root@{{IP}}
```

4. Creamos el script de instalación
	`touch /tmp/install.sh`

5. Copiamos el contenido del script 
	script: `install_production_standard.sh`
	ubicación: `github dev-tools rama main`
	url: [github/dev-tools](https://github.com/puntsistemes/dev-tools_odoo/blob/main/install_production_standard.sh)


6. Damos permisos de ejecución al script y lanzamos
	- `chmod +x /tmp/install.sh`
	- `./install.sh`
	![[Pasted image 20240507103907.png]]

7. Completamos la información que pide el script
	- dns producción
	- dns desarrollo
	- usuario y token para enterprise

8. Crear 2 entradas de passwords (`desarrollo` y `produccion`) ==> ODOO bundle

	![[Pasted image 20240507173801.png]]

1. Crear `aliases` y `ssh` en `dev-tools` para el cliente nuevo

- `dev-tools/helpers/.bash_aliases`
```bash
alias ftm_dev='_get_client_db ftm 5433 DEV FTM_DEV 17E'  
alias ftm_pro='_get_client_db ftm 5432 PRO FTM_PRO 17E'
```
- `dev-tools/helpers/config`
```bash
Host coelbe  
    HostName coelbe.puntsistemes.cloud  
    IdentityFile ~/.ssh/ssh_key_private  
    Port 2228  
    SetEnv LC_ALL=C.UTF-8  
    User odoo
```

> [!IMPORTANT]
> Antes de salir del server (despues de la instalacion)  añadir alias para ssh en cliente

> [!DANGER]
> Si nos equivocamos con el `dominio` durante la instalación, lo podemos resolver así
> [[Error instalación con Domino DNS equivocado]]

