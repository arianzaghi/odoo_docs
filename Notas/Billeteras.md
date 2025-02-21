> [[Modulos custom de punt]]

Tags: 
Status: 
Related: 

___

# Billeteras

# Docum

## **Descripción General del Sistema**

El módulo de Odoo permitirá gestionar múltiples billeteras de compra-venta de criptomonedas. Cada billetera contendrá diferentes "assets", uno por cada tipo de moneda, que registrarán tanto la cantidad total disponible como el precio medio de compra de cada asset. El sistema permitirá registrar transacciones de diferentes tipos: **compra**, **venta** y **transferencia** de assets entre billeteras.

Este documento describe en detalle la estructura del sistema y la lógica para manejar transacciones, en especial el flujo de transferencias entre billeteras, que se registrarán en ambas billeteras para asegurar la máxima trazabilidad.

---

## **1. Entidades Principales del Sistema**

### **1.1 Billetera (Wallet)**

- Identificador único (ID)
- Nombre de la billetera
- Usuario propietario
- Relación uno-a-muchos con **Asset**
- Relación uno-a-muchos con **Transaction**

### **1.2 Asset** (Moneda en la billetera)

- Identificador único (ID)
- Tipo de moneda (BTC, ETH, USDT, etc.)
- Cantidad total disponible
- Precio medio de compra
- Relación muchos-a-uno con **Wallet**

### **1.3 Transaction** (Transacción)

- Identificador único (ID)
- Tipo de transacción: **Compra**, **Venta**, **Transferencia - Salida**, **Transferencia - Entrada**
- Moneda (BTC, ETH, etc.)
- Cantidad
- Precio unitario (en caso de compra o venta)
- Fecha de la transacción
- Relación muchos-a-uno con **Wallet de origen**
- Relación muchos-a-uno con **Wallet de destino** (solo para transferencias)

---
## **2. Tipos de Transacciones y su Lógica**

### **2.1 Compra**

- **Descripción:** Aumenta el saldo del asset en la billetera correspondiente.
- **Acciones:**
    - Sumar la cantidad comprada al saldo existente.
    - Recalcular el precio medio de compra utilizando el precio de la nueva transacción.

### **2.2 Venta**

- **Descripción:** Reduce el saldo del asset en la billetera.
- **Acciones:**
    - Restar la cantidad vendida del saldo existente.
    - No afecta el precio medio de compra.

### **2.3 Transferencia**

- **Descripción:** Mueve una cantidad específica de un asset de una billetera a otra. Se registra en ambas billeteras para asegurar la trazabilidad.
- **Acciones:**
    1. Validación:
        - Verificar que la billetera de origen tenga saldo suficiente del asset.
        - Asegurar que las billeteras de origen y destino sean distintas.
    2. Registrar la transferencia en ambas billeteras:
        - **En la billetera de origen:** Crear una transacción de tipo **Transferencia - Salida**. Restar la cantidad del asset.
        - **En la billetera de destino:** Crear una transacción de tipo **Transferencia - Entrada**. Sumar la cantidad al asset.
    3. Mantener el historial de transacciones sincronizado entre ambas billeteras.        

---

## **3. Cálculo del Precio Medio de Compra**

El precio medio de compra se recalcula en cada operación de **compra** o al recibir una **transferencia - entrada**. La fórmula es la siguiente:

```
Nuevo precio medio = (Cantidad existente × Precio medio actual + Nueva cantidad × Precio de la transacción) / (Cantidad existente + Nueva cantidad)
```

Nota: En las transferencias, el precio medio de la billetera de origen no se modifica.

---

## **4. Flujo de Transferencias: Ejemplo Práctico**

### **Escenario:**

- Moneda: BTC
- **Billetera A:** 2 BTC con precio medio de 30,000 USD.
- **Billetera B:** 1 BTC con precio medio de 40,000 USD.
- Se transfiere 0.5 BTC de la Billetera A a la Billetera B.

### **Antes de la Transferencia:**

- **Billetera A:** 2 BTC, precio medio 30,000 USD.
- **Billetera B:** 1 BTC, precio medio 40,000 USD.

### **Después de la Transferencia:**

- **Billetera A:** 1.5 BTC, precio medio 30,000 USD.
- **Billetera B:** 1.5 BTC, precio medio ajustado:

```
Nuevo precio medio = [(1 × 40,000) + (0.5 × 30,000)] / (1 + 0.5) = 36,666.67 USD
```

---

## **5. Diagrama de Flujo del Proceso de Transferencia**

---

## **6. Validaciones y Consideraciones Adicionales**

### **6.1 Validaciones:**

- Asegurar que la cantidad transferida no exceda el saldo disponible.
- Verificar que las billeteras de origen y destino sean distintas.

### **6.2 Manejo de Errores:**

- Si ocurre un error durante la transferencia, se debe revertir cualquier cambio parcial para evitar inconsistencias.

### **6.3 Sincronización y Performance:**

- Garantizar que el sistema maneje transacciones simultáneas de forma consistente utilizando bloqueos o colas de procesamiento.
    

---

## **7. Conclusión**

Este módulo proporciona una gestión completa y trazable de activos de criptomonedas en múltiples billeteras, asegurando que todas las transacciones, especialmente las transferencias, estén registradas de manera coherente y auditables. Registrar las transferencias en ambas billeteras ofrece la máxima trazabilidad y facilita la gestión de los fondos de manera precisa.

¿Próximo paso? Implementar la lógica de este sistema en código y definir la interfaz para los usuarios finales en Odoo. 😊