> [[059 - Configuracion y Estructura]]

Tags: 
Status: 
Related: 

___

# Ajustes de odoo
> Los ajustes de odoo nos permiten añadir configuraciones y parametrizaciones desde los apartados de cada modelo de odoo.

![[Pasted image 20241126114706.png]]
## Bloque de ajustes para vista
```xml
<record id="pnt_res_config_settings_view_form" model="ir.ui.view">
	<field name="name">res.config.settings.view.redirect.app</field>
	<field name="model">res.config.settings</field>
	<field name="priority" eval="40"/>
	<field name="inherit_id" ref="hr_attendance.res_config_settings_view_form"/>
	<field name="arch" type="xml">
		%% Indicamos el apartado de los ajustes %%
		<xpath expr="//form//app[@name='hr_attendance']" position="inside">
			<block title="{{TITLE}}" name="extra_hours_coefficient">
				<setting string="Active Ponderation Period" company_dependent="1">
					<field name="selected_coefficient_id" class="w-75"/>
					<group>
						<field name="pnt_extra_ponderation" readonly="1"/>
						<field name="pnt_festive_ponderation" readonly="1"/>
						<field name="pnt_night_ponderation" readonly="1"/>
					</group>
					<group>
						<field name="pnt_period_init_date" readonly="1"/>
						<field name="pnt_period_end_date" readonly="1"/>
					</group>
				</setting>
			</block>
		</xpath>
	</field>
</record>
```
## [[Ajustes basicos para modulo de odoo]]
## [[Añadir ajustes para módulo odoo]]