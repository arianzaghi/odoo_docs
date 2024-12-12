> [[Tipos de Vistas]]

Tags: #todo
Status: 
Related: 

___

# Vista Form - Formulario

## [[Componentes estructurales xml form]]


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