> [[080 - BBDD]]

Tags:
Status: 
Related: 

___
# 🌱 **Clonar la base de datos del Docker de GitHub**


> [!INFO] Quick Info
> `database_pulls {{contenedor}} {{nombre_local}}`

### 1️. **Obtener el nombre del contenedor**

> A partir de la URL del Docker, elimina `https://` y el dominio para quedarte solo con el nombre del contenedor.

- **Ejemplo:**  
    **URL:** `https://som-energia_odoo_1_puntsistemes.pulls.puntsistemes.cloud`  
    **Contenedor:** `som-energia_odoo_1_puntsistemes`

---
### 2️. **Ejecutar el comando**

> Utilizamos el comando `database_pulls` en la terminal:

```sh
database_pulls {{CONTENEDOR}} {{NOMBRE_BBDD_PARA_GUARDARLO}}
```

- **DOMINIO:** Nombre del contenedor (`som-energia_odoo_1_puntsistemes`)
- **NOMBRE_BBDD_PARA_GUARDARLO:** El nombre local de la base de datos.

---
### 🔧 **Ejemplo rápido:**

```
database_pulls som-energia_odoo_1_puntsistemes som-energia_1
```

> Esto clonará la base de datos y la guardará como `som-energia_1`.
