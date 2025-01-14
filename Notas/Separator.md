> [[Back]]

Tags: 
Status: 
Related: 

___

# Separator

Todos los elementos que esten dentro de un mismo `separator`, iran con `or`. Los que esten en distintos separatos, `and`

```xml
<record id="pnt_expense_view_search" model="ir.ui.view">  
    <field name="name">tb.expense.view.search</field>  
    <field name="model">tb.expense</field>  
    <field name="arch" type="xml">  
        <search string="Search Expenses">  
            <field string="Category OR" name="category_ids"/>  
            <separator/>  
            <field string="Category AND" name="category_ids"/>  
            <separator/>  
        </search>  
    </field>  
</record>
```