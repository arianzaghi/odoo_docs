> [[031 - Elementos de Interfaz]]

Tags: #todo
Status: 
Related: 

___
# Menu Item
> Botones anidados y con jerarquía que se encuentran en el top navbar.

> [!WARNING] Security
> Para modelos que no sean core, debemos añadirlos al security [[050 - Security]], sino no podremos visualizarlos

![[Pasted image 20240205174931.png]] ^04f58e

```python
<menuitem id="res_partner_menu_config"  
    name="Configuration"  
    parent="menu_contacts"  
    groups="base.group_system"  
    sequence="2"
/>
```

## [[Menu Item Padre]]
## [[Menu Item Hijo]]

