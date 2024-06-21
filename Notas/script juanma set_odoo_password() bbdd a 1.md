> [[Bash y scripts]]

Tags: 
Status: 
Related: 

___

# script juanma set_odoo_password() bbdd a 1
>Script para actualizar la contraseña de la bbdd de odoo

```bash
function set_password_odoo() {
  case "$#" in
    0)
      echo "Tienes que poner la base de datos"
      ;;
    1)
      docker exec -it postgres psql -U odoo "$1" -c "UPDATE res_users SET password=1 WHERE id=2;"
      ;;
    2)
      docker exec -it postgres psql -U odoo "$1" -c "UPDATE res_users SET password=1 WHERE login='$2';"
      ;;
    *)
      echo "Esta función solo admite 1 o 2 parámetros"
      ;;
  esac
}

```