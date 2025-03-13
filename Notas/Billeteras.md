> [[Modulos custom de punt]]

Tags: 
Status: 
Related: 

___

# Billeteras

## **Módulo Billeteras**

### **Descripción General del Sistema**

El módulo de Odoo permitirá gestionar múltiples billeteras de compra-venta de criptomonedas (**pt.wallet**), con transacciones y activos asociados.

Cada billetera puede tener múltiples transacciones (**pt.transaction**), las cuales registran:

- Precio de compra
- Cantidad
- Fecha
- Valor y moneda
- Estado (borrador o confirmada)
- Tipo (compra o venta)

Para cada grupo de transacciones en estado confirmado de una misma moneda, se crea un registro de tipo **asset** que guarda los totales de esa moneda (**pt.asset**). Cada asset registra:

- Cantidad
- Precio medio de compra
- Valor total
- Indicador booleano: **Es USDT**

El asset USDT es de carácter especial y representa la cantidad de moneda estable disponible en la billetera (**liquidez**). Su funcionamiento es el siguiente:

- Cuando se compra cualquier tipo de moneda, el valor de la transacción se resta del asset USDT.
- Cuando se vende cualquier tipo de moneda, la ganancia de la transacción se acumula en el asset USDT.
- Todas las operaciones de compra de USDT representan un ingreso de liquidez en la billetera.

### **Estructura del Sistema**

#### **Billeteras (pt.wallet)**

Cada billetera gestiona su propio balance de criptomonedas.

#### **Transacciones (pt.transaction)**

Las transacciones representan operaciones de compra o venta de criptomonedas e incluyen:

- Precio de compra
- Cantidad
- Fecha
- Valor
- Moneda
- Estado (borrador/confirmada)
- Tipo (compra/venta)

#### **Activos (pt.asset)**

Cada billetera tiene un asset por cada moneda, calculando:

- Cantidad
- Precio medio de compra
- Valor total

Los assets **no tienen relación directa con las transacciones mediante campos**, sino que se recalculan dinámicamente. Este recalculado se ejecuta automáticamente al crear, modificar o eliminar transacciones.

### **Funcionamiento**

#### **Compras/Ventas**

- Todas las operaciones se realizan exclusivamente contra USDT. No existen conversiones directas entre criptomonedas.

#### **Validación de Saldo**

- Si no hay suficiente USDT para una compra o saldo suficiente de una criptomoneda para una venta, la transacción queda en borrador.
- No se permite confirmar compras sin liquidez en USDT.
- Las compras de USDT no descuentan saldo de ningún asset.

#### **Recalculado de Assets**

- Cada billetera tiene un único asset por moneda, calculando el precio medio de compra y la cantidad disponible.
- El recalculado de assets se ejecuta automáticamente al crear, modificar o eliminar transacciones.
- Cuando se crea una nueva transacción de compra, se debe comprobar que existe balance suficiente en USDT para comprar la moneda.
- Cuando se crea una nueva transacción de venta, se debe comprobar que existe balance suficiente de esa moneda para venderla.
- Si se modifican transacciones y hay un incremento del valor de compra/venta, debe existir saldo suficiente de USDT/moneda. Si no lo hay, la transacción se mantendrá en estado **borrador**.

### **Datos Clave**

- Liquidez representada por el asset **USDT** en cada billetera.
- Ganancas/Perdidas Calculadas en base al precio medio de compra del asset.
- EL ROI Se obtiene comparando el precio medio de compra con el precio actual del mercado.

### **Funcionalidades de la Aplicación**

La aplicación permitirá:

- Ver en tiempo real el saldo de USDT y del resto de monedas.
- Ver el precio medio de compra de todas las monedas.
- Ver el total invertido, el total de ganancias (o pérdidas) y las ganancias netas.

Este sistema proporcionará una visión clara y actualizada del saldo de cada billetera, permitiendo tomar decisiones estratégicas sobre la compra y venta de criptomonedas.