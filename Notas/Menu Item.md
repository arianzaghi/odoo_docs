> [[Odoo Views Vistas]]

Tags:
Status: 
Related: 

___
# Menu Item
Botones anidados y con jerarquía que se encuentran en el top navbar

![[Pasted image 20240205174931.png]]

```python
<menuitem id="res_partner_menu_config"  
    name="Configuration"  
    parent="menu_contacts"  
    groups="base.group_system"  
    sequence="2"/>
```

# Añadir Menu Item

## 1. Identificar el `menu-item` Padre

Para agregar un nuevo ítem al menú, primero debemos localizar el `ref` del `menu-item` padre en el que deseamos insertar nuestra nueva entrada.

- **Localizar el `ref` del `menu-item` Padre:**
  1. Inspeccionamos elemento (F12)
  2. Nos situamos sobre el menu-item en el que queremos añadir una entrada
  3. Buscamos la referencia XML dentro de los elementos del código HTML.

![[Pasted image 20240206112319.png]]

### 2. Heredar del Menú Original para Añadir el Nuevo `menu-item`

1. **Definir la Acción del Menú:**
	Primero, definimos la acción que ejecutará nuestro botón mediante `ir.actions.act_window`. Este paso involucra asignar un ID único a nuestra acción (marcado como B en el ejemplo) y especificar el modelo y la vista que se utilizarán.

```python
<record id="pnt_res_partner_hobbies_action" model="ir.actions.act_window">  
    <field name="name">Hobbies and skills</field>  
    <field name="res_model">pnt.res.partner.hobbies</field>  
    <field name="view_mode">tree,form</field>  
    <field name="help" type="html">  
        <p class="o_view_nocontent_smiling_face">No items created.</p>  
    </field>  
</record>
```

- **Insertar el Nuevo `menu-item`:**
	A: `id` del record actual
	B: `id` de la acción de menú
	C: `ref` del `menu-item` padre 

```python
<record id="A(pnt_new_sale_menu)" model="ir.ui.menu">
    <field name="name">PNT NEW BUTTON</field>
    <field name="action" ref="B(pnt_new_button_action)"/>
    <field name="parent_id" ref="C(sale.sale_order_menu)"/>
    <field name="sequence">22</field>
</record>
```

## 3. Verificación

- Para verificar que los nuevos menu item han sido añadidos correctamente nos dirigimos a:
	`Ajustes > Técnico > Elementos de menú (menuitems)`


## Referencias

- [Documentacion](https://www.odoo.com/documentation/16.0/es/developer/howtos/website_themes/navigation.html?highlight=menu%20item#menu-item)


