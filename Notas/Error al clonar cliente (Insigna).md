> [[Errores]]

Tags: 
Status: 
Related: 

___

# Error al clonar cliente

> Error en Insigna

> [!ERROR]
> Al realizar el client mirror y lanzarlo en nuestro local, vemos error en TODAS las librerias.

**Problema:**
- Los repositorios de `/odoo110/src/` son solo carpetas, y no contienen repositorio.
- Cuando hacemos el `git_log`, al no tener repositorios en las carpetas, se hace mal
- Al hacer el `client_mirror` no se actualizan correctamente los módulos

**Solución:**
- Usar un client mirror antiguo
- Restablecerlo en el equipo local
- Mover todos los repositorios del local al servidor