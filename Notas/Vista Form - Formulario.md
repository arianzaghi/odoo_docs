> [[032 - Tipos de Vistas]]

Tags: #todo
Status: 
Related: 

___
# Vista Form - Formulario

![[Pasted image 20241212172759.png]] ^606814
```xml
<record id="{{NAME}}_view_form" model="ir.ui.view">  
    <field name="name">{{MODULE.}}.view.form</field>  
    <field name="model">{{MODULE.}}</field>  
    <field name="arch" type="xml">  
        <form string="Item detail" class="o_sale_order" create="false">  
            <header>  
	            <label for="{{field1}}" string="{{String1}}"/>  
				<h1>  
					<field name="{{field1}}" readonly="True"/>  
				</h1>  
            </header>  
            <sheet>  
                <group>  
                    <field name="{{field2}}"/>  
                    <field name="{{field3}}"/>  
                </group>  
                <group>  
                    <field name="{{field4}}"/>  
                </group>  
            </sheet>  
        </form>  
    </field>  
</record>
```

## Ejemplos Herencias
### Res Partner Contacto

#### Campo debajo de direccion entrega
![[Pasted image 20250508125251.png]]

```xml
<xpath expr="//group[//field[@name='vat']]" position="before">  
    <group>  
        <field name="pnt_christmas_review"  
               invisible="company_type != 'company'"/>  
        <field name="pnt_christmas_shipping"  
               invisible="not pnt_christmas_review"/>  
        <field name="pnt_christmas_shipping_type"  
               invisible="type != 'christmas'"  
               required="type == 'christmas'"/>  
    </group>  
</xpath>
```

### Sale Order Form
### Purchase Order Form