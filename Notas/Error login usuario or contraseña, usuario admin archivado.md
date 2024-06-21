> [[Errores]]

Tags: 
Status: 
Related: 

___

# Error login usuario or contraseña

> **PROBLEMA:** El cliente no puede iniciar sesión en odoo. Recibe el siguiente error: "Usuario o contraseña incorrectos"

> **CAUSANTE**: El usuario admin ha sido archivado por otro usuario con privilegios, y cuando busca las credenciales introducidas en la BBDD para comprobar si existe, no encuentra la entrada de admin porque esta archivado-

## `psql PRO`
![[Pasted image 20240523105856.png]]

## **Localizamos usuario admin**
```sql
select id,login,active from res_users where login='admin';
```

## Actualizamos estado `active`
```sql
UPDATE res_users SET active='t' WHERE login='admin';
```