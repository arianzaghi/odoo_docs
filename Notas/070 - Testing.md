> [[010 - Odoo HOME]]

Tags: 
Status: 
Related: 

___

# 070 - Testing

## **Lanzar tests**
`odoo-bin -d db_name --test-enable --stop-after-init -i/u modulo --log-level=test`
![[Pasted image 20241218103246.png]]

## **¿Cómo se crean los test?**
- Importamos la clase `TransactionCase` de `odoo.test.common`
- Definimos datos comunes en la función `setUp()` o `setUpclass`
- Solo se ejecutarán como test las funciones con test_nombre_función
- Podemos heredar otra clase de test y tener todo lo que tenían, pero solo es recomendable heredar configuración

## **Buenas Prácticas (OCA)**
- No utilizar datos demo de otros módulos. Otros módulos pueden cambiar los datos.Todos los archivos de prueba deben añadirse en `some_addon/tests/`
- Definir datos demo si los necesitamos. Ayudaran a probar funcionamiento el módulo más fácilmente por interfaz y los podremos   en los tests
- No utilizar usuarios ya existentes en los tests (excepciones).
- No utilizar Form() en todo, pero si en lo útil (pedidos de ventas, compra, facturas, etc).
- No comparar con variables, comparar siempre con valores directamente.
- Definir métodos para llamarlos en los tests, por ejemplo, creación de pedidos.
- Cuidado con definir defaults en los contextos de los tests.

## [[Ejemplo Tests]]

## Flujo Generacion de Test

1. Seleccionamos la clase entera que queremos testear y le pedimos a copilot que genere el SetUp() para esa clase
2. 