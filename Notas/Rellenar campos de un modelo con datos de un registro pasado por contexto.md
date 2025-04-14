> [[Contextos]]

Tags: 
Status: 
Related: 

___

# Rellenar campos de un modelo con datos de un registro pasado por contexto

> Historia de juanma. Se esta creando una venta, se le pasa una oportunidad por contexto, y queremos rellenar los campos de la venta usando campos del registro que hemos pasado por contexto

> En la accion se pasa la oportunidad por contexto, y en el record se asignan default.
```python
  <record id="sale_action_quotations_new" model="ir.actions.act_window">  
<field name="name">Quotation</field>  
<field name="res_model">sale.order</field>  
<field name="view_mode">form,tree,graph</field>  
<field name="domain">[('opportunity_id', '=', active_id)]</field>  
<field name="context">{'search_default_opportunity_id': active_id, 'default_opportunity_id': active_id}</field>  
</record>

    <record id="sale_view_inherit123" model="ir.ui.view">  
<field name="name">sale.order.form.inherit.sale</field>  
<field name="model">sale.order</field>  
<field name="inherit_id" ref="sale.view_order_form"/>  
<field name="arch" type="xml">  
<xpath expr="//field[@name='origin']" position="after">  
<field name="opportunity_id" context="{  
                    'default_campaign_id': campaign_id,  
                    'default_company_id': company_id,  
                    'default_medium_id': medium_id,  
                    'default_partner_id': partner_id,  
                    'default_source_id': source_id,  
                    'default_tag_ids': tag_ids,  
                    'default_type': 'opportunity',  
                }"/>  
</xpath>  
</field>  
</record>
```