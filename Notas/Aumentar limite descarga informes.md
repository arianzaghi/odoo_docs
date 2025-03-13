> [[090  - Servidor gestion]]

Tags: 
Status: 
Related: 

___

# Aumentar limite descarga facturas

> **Problema:** Odoo nos impide imprimir más de 80 facturas al mismo tiempo
> **Solución:** Aumentar el espacio de RAM asignado en el `.conf` del servidor

```sh
limit_memory_hard = 14294967296
limit_memory_soft = 13221225472
```

1. Cambiamos valores del `.conf` en `DEV` y en `PRO`
2. Reiniciamos servidores