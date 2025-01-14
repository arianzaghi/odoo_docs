> [[Search View]]

Tags: 
Status: 
Related: 

___

# Filtros estaticos Search View

- **date="pnt_date"**: Filtro fecha por defecto
## [[Separator]]


## Ejemplo plantilla
```xml
<record id="pnt_view_daily_extra_hour_detail_search" model="ir.ui.view">  
    <field name="name">pnt.extra.hour.detail.search</field>  
    <field name="model">pnt.extra.hour.detail</field>  
    <field name="arch" type="xml">  
		<search string="Search Extra Hours Detail">
		# ...
		</search>  
    </field>
</record>

<record id="pnt_extra_hour_detail_action" model="ir.actions.act_window">  
    <field name="name">Extra Hours Detail</field>  
    <field name="res_model">pnt.extra.hour.detail</field>  
    <field name="view_mode">pivot,form</field>  

	%% Referencia a search y contexto filtro por defecto %%
    <field name="search_view_id" ref="pnt_view_daily_extra_hour_detail_search"/>  
    <field name="context">{'search_default_{{FILTER_NAME}}': 1}</field>  
    
    <field name="help" type="html">  
        <p class="o_view_nocontent_smiling_face">No items created.</p>  
    </field>
</record>
```

### Filtro de Fecha
> ![[Pasted image 20250103133127.png]]

```xml
<filter string="Date" name="filter_create_date" date="pnt_date"/>
```

### `MONTH to DATE` Filtrar registros desde inicio de mes hasta hoy
```xml
<filter string="Month to Date"  
        name="filter_this_month_to_date"  
        domain="[('pnt_date', '&gt;=', (context_today() - datetime.timedelta(days=context_today().day - 1)).strftime('%Y-%m-%d')),  
        ('pnt_date', '&lt;=', context_today().strftime('%Y-%m-%d'))]"/>
```

### `YEAR to DATE` Filtrar registros desde inicio de año hasta hoy
```xml
<filter string="Year to Date"  
        name="filter_this_year_to_date"  
        domain="[('pnt_date', '&gt;=', (context_today() - datetime.timedelta(months=context_today().month - 1)).strftime('%Y-%m-%d')),  
                ('pnt_date', '&lt;=', context_today().strftime('%Y-%m-%d'))]"/>
```