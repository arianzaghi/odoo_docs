 > [[Odoo Modelos]]

Tags: #todo 
Status: 
Related: 

___

# Wizards

## Wizard Avanzado

[[Wizard Impresion Etiqueta Rellenando Campos]]
[[Wizard impresión Etiquetas desde Albarán con Lotes]]

## Ejemplo de wizard Classic

> Modelo: `stock.immediate.transfer`
> Ref externa: `stock.view_immediate_transfer`
> path: `src/core/addons/stock/wizard`

```python
<?xml version="1.0" encoding="UTF-8"?>  
<odoo>  
    <record id="view_immediate_transfer" model="ir.ui.view">  
        <field name="name">stock.immediate.transfer.view.form</field>  
        <field name="model">stock.immediate.transfer</field>  
        <field name="arch" type="xml">  
            <form string="Immediate transfer?">  
                <group>  
                    <p>  
                        You have not recorded <i>done</i> quantities yet, by clicking on <i>apply</i>  
                        Odoo will process all the <i>reserved</i> quantities.  
                    </p>  
                </group>  
                <footer>  
                    <button name="process" string="_Apply" type="object" class="btn-primary"/>  
                    <button string="Cancel" class="btn-secondary" special="cancel" />  
                </footer>  
            </form>  
        </field>  
    </record>  
</odoo>
```

## Wizard Sencillo
- [[popup confirmación]]

