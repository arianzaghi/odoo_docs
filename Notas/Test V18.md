
🛠️ Cambios importantes en el desarrollo con Odoo 18 respecto a la carga de tests:  
Desde Odoo 18, se han introducido cambios relevantes en cómo deben organizarse los módulos, en especial respecto al uso del framework de tests y la estructura del código. A continuación, se detallan las principales recomendaciones y advertencias que hay qye seguir en nuestros desarrollos:  
  
✅ 1. Uso del framework de tests (from odoo.tests import Form)  
Desde la versión 12, Odoo introdujo el uso de Form (y otros elementos del framework de tests) para facilitar la simulación de formularios.  
  
➡️ Aunque técnicamente se podía usar en cualquier parte, su uso estaba pensado exclusivamente para entornos de pruebas (tests/).  
➡️ Hasta Odoo 17 esto no generaba errores, aunque su uso fuera inapropiado.  
  
🔴 A partir de Odoo 18, si se importa Form o cualquier parte del framework de tests desde módulos de negocio (models, controllers, etc.), se lanza un error o warning como el siguiente:  
  
odoo.tests.common: Importing test framework, avoid importing from business modules and when not running in test mode  
Stack (most recent call last):  
File "/opt/sources/odoo180/src/core/odoo-bin", line 8, in <module>  
odoo.cli.main()  
File "/opt/sources/odoo180/src/core/odoo/cli/command.py", line 66, in main  
o.run(args)  
File "/opt/sources/odoo180/src/core/odoo/cli/server.py", line 182, in run  
main(args)  
File "/opt/sources/odoo180/src/core/odoo/cli/server.py", line 175, in main  
...  
  
🚩 Por tanto:  
Aunque aun está permitido, no es recomendado usar el framework de tests fuera de archivos ubicados en tests.  
  
✅ 2. Estructura del paquete de tests  
Desde la versión 15, Odoo ya no requiere (ni recomienda) importar explícitamente el paquete tests desde el __init__.py principal del módulo.  
  
📌 Ejemplo incorrecto en mi_modulo/__init__.py:  
  
from . import tests # ❌ No necesario, y ahora desaconsejado  
  
📌 A partir de Odoo 18, esta práctica lanza un warning en tiempo de carga, similar al anterior, porque provoca la carga del framework de tests fuera del entorno controlado.  
  
✔️ Lo correcto es dejar que Odoo descubra/cargue automáticamente los tests ubicados en el subdirectorio tests/ y hacer los imports desde los tests si es necesario.  
  
🧪 Alternativa a Form en la capa de negocio  
Si necesitas simular lógica de formulario (por ejemplo, para disparar @api.onchange) desde código de negocio, se puede usar la API de creación temporal de registros:  
  
record = self.env['sale.example'].new({  
'field1': 'value',  
'field2': 'value',  
})  
record._onchange_some_field()  
record._onchange_some_field2()  
values = record._convert_to_write(record._cache)  
created = self.env['sale.example'].create(values)  
  
⚠️ Aunque esta alternativa no es tan conveniente como Form, es la forma correcta y segura de manejar estos casos a partir de Odoo 18. Es probable que en futuras versiones (19+) el uso indebido del framework de tests sea aún más restringido.  
  
🛍️ Resumen desde Odoo 18:  
❌ No importar tests en __init__.py del módulo.  
❌ No usar Form ni ningún componente del framework de tests fuera del directorio tests/.  
✔️ Para simular formularios en la capa de negocio, se puede usar new() + _onchange_ + _convert_to_write().