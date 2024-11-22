> [[Contextos]]

Tags: 
Status: 
Related: 

___

# Llamar un método con contexto

> Cuando creo un PV y lo confirmo, automáticamente se crean los PC.
> Queremos que se haga a través de un botón.

**Botón que llama al método**
```xml
<button name="action_quotation_send" position="after">  
    <button name="action_generate_purchase_order" string="Generate Purchase Order" type="object" class="oe_highlight" invisible="state != 'sale'"/>  
</button>
```

**Desde la llamada**
> Defino en el modelo en el que quiero hacer la llamada al método
```python
def action_generate_purchase_order(self):  
    for order in self:  
		# Añadimos el registro a order (o self)
        order = order.with_context({'is_confirmed_by_user': True})  
        # Llamamos al método de forma normal
        order.order_line.sudo()._purchase_service_generation()
```

**Desde el método**
> En este caso, heredo un método del modelo de odoo `sale_purchase` para limitar desde donde se llama
```python
def _purchase_service_generation(self):  
    # Si se ha llamado al método desde algun sitio que no sea nuestro boton, no lo ejecutamos
    is_confirmed = self.env.context.get('is_confirmed_by_user')  
    if is_confirmed:  
        return super(SaleOrderLine, self)._purchase_service_generation()  
    return
```