> [[Back]]

Tags: 
Status: 
Related: [[sale_purchase]]

___

# Generar pedidos de compra authenticate a través de una venta


✅ PV debe tener asignada una cuenta analítica antes de generar el pedido de compra
✅ cada producto en el pedido debe tener un proveedor asignado antes de generar un pedido de compra
✅ que se genere una solicitud de compra en estado "SdP" para cada proveedor con productos en el pedido
✅ Los productos deben acumularse en la solicitud de compra existente
✅ que las solicitudes de compra generadas hereden la cuenta analítica del pedido de venta origen
✅ la cuenta analítica debe mostrarse en la pestaña "Otra información" de la solicitud de compra
✅ Quiero que los productos duplicados en una solicitud de compra acumulen sus cantidades en la primera línea