> [[Errores]]

Tags: 
Status: 
Related: 

___

# Error arrancar FluidThermal FTM

```bash
pip install 'lxml<5'
pip install urllib3==1.26.16

```

```python
/usr/local/bin/python3.10 /opt/sources/odoo170/src/core/odoo-bin -c /opt/sources/odoo170/conf/fluidthermal.conf -d FTM_PRO 
Traceback (most recent call last):
  File "/opt/sources/odoo170/src/core/odoo-bin", line 5, in <module>
    import odoo
  File "/opt/sources/odoo170/src/core/odoo/__init__.py", line 134, in <module>
    from . import modules
  File "/opt/sources/odoo170/src/core/odoo/modules/__init__.py", line 8, in <module>
    from . import db, graph, loading, migration, module, registry, neutralize
  File "/opt/sources/odoo170/src/core/odoo/modules/graph.py", line 11, in <module>
    import odoo.tools as tools
  File "/opt/sources/odoo170/src/core/odoo/tools/__init__.py", line 24, in <module>
    from .mail import *
  File "/opt/sources/odoo170/src/core/odoo/tools/mail.py", line 32, in <module>
    safe_attrs = clean.defs.safe_attrs | frozenset(
AttributeError: module 'lxml.html.clean' has no attribute 'defs'
```