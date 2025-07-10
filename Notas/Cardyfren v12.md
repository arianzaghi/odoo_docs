> [[Migraciones]]

Tags: 
Status: 
Related: 

___

# Cardyfren v12

1. ✅ Buscamos módulos no instalados en PRO para descartarlos
	 Todos instalados, no hay ninguno descartable
2. ✅[[Script de módulos en Servidor Cardyfren]]
3. ✅ Pasar Pro a **DEV_MIGRACION** y borrar módulos delicados a ver que pasa
	1. ✅Jasper Controller **FUERA**
	2. ✅Blackbox **FUERA**
	3. POB (Prestashop OPdoo Bridge) **Se queda talcual**
		1. Son comprados, hay que revisar si estan modificados
			1. **pob**
			2. **pob_extension_stock**
			3. **prestaerp**
	4. Modulos oca a pelo (ver si estan en 17, y de donde vienen para saber si estan modificados)
		1. tarifa_lista_materiales_pnt
		2. purchase_allowed_product (MODIFICADO)
			1. En v17 SI
			2. En v18 No
		3. purchase_invoicing_no_zero_line
			1. No esta en v12, solo v13
			2. Solo hasta v16
		4. Purchase Picking State
			1. Solo hasta la v14
			2. https://github.com/OCA/purchase-workflow/tree/14.0/purchase_picking_state


## Pasos del a migracion
1. **Migramos de 12 a 16 mediante comando odoo**
2. Arrancamos v16 con -u all
	1.  /opt/sources/odoo160/src/core/addons/sale_delivert_state/views/sale_order_views.xml
	2. /opt/sources/odoo160/src/enterprise/account_reports/views/res_company_views.xml
	3. /opt/sources/odoo160/src/l10n-spain/l10n_es_aeat/views/res_company_view.xml
	4. /opt/sources/odoo160/src/core/addons/sale_stock/views/sale_order_views.xml
	5. /opt/sources/odoo160/src/sale-workflow/sale_delivery_state/views/sale_order_views.xml
	6. /opt/sources/odoo160/src/sale-workflow/sale_partner_incoterm/views/sale_order.xml
	7. /opt/sources/odoo160/src/core/addons/sale_timesheet/views/sale_order_views.xml
	8. /opt/sources/odoo160/src/core/addons/stock_dropshipping/views/sale_order_views.xml
	9. /opt/sources/odoo160/src/purchase-workflow/purchase_discount/views/purchase_discount_view.xml
	10. /opt/sources/odoo160/src/purchase-workflow/purchase_request/views/purchase_order_view.xml
	11. /opt/sources/odoo160/src/account-analytic/purchase_analytic/views/purchase_views.xml
	12. /opt/sources/odoo160/src/purchase-workflow/purchase_force_invoiced/view/purchase_order.xml
	13. /opt/sources/odoo160/src/purchase-workflow/purchase_order_type/views/view_purchase_order.xml
	14. /opt/sources/odoo160/src/core/addons/purchase_stock/views/purchase_views.xml
	15. /opt/sources/odoo160/src/bank-payment/account_payment_purchase/views/purchase_order_view.xml
	16. /opt/sources/odoo160/src/sale-workflow/sale_order_type/views/sale_order_view.xml
	17. /opt/sources/odoo160/src/purchase-workflow/purchase_landed_cost/views/purchase_order_view.xml
	18. /opt/sources/odoo160/src/core/addons/purchase_mrp/views/purchase_order_views.xml
	19. /opt/sources/odoo160/src/purchase-workflow/purchase_partner_incoterm/views/purchase_view.xml
	20. /opt/sources/odoo160/src/account-invoicing/purchase_stock_picking_return_invoicing/views/purchase_view.xml
	21. /opt/sources/odoo160/src/core/addons/sale_purchase/views/purchase_order_views.xml
	22. /opt/sources/odoo160/src/purchase-workflow/purchase_order_line_sequence/views/purchase_view.xml
	23. /opt/sources/odoo160/src/core/addons/stock_dropshipping/views/purchase_order_views.xml
	24. /opt/sources/odoo160/src/core/addons/purchase/views/res_config_settings_views.xml
	25. /opt/sources/odoo160/src/core/addons/purchase/views/res_partner_views
	26. /opt/sources/odoo160/src/core/addons/purchase/report/purchase_report_views.xml
	27. /opt/sources/odoo160/src/purchase-workflow/purchase_order_type/views/view_purchase_order_type.xml
	28. /opt/sources/odoo160/src/purchase-workflow/purchase_landed_cost/views/purchase_cost_distribution_view.xml
	29. /opt/sources/odoo160/src/purchase-workflow/purchase_request/views/purchase_request_view.xml
	30. /opt/sources/odoo160/src/purchase-workflow/purchase_request/views/purchase_request_line_view.xml
	31. /opt/sources/odoo160/src/enterprise/purchase_enterprise/report/purchase_report_views.xml
	32. /opt/sources/odoo160/src/core/addons/purchase_stock/views/res_config_settings_views.xml
	33. /opt/sources/odoo160/src/core/addons/purchase_stock/views/res_partner_views.xml
	34. /opt/sources/odoo160/src/core/addons/purchase_stock/report/purchase_report_views.xml
	35. /opt/sources/odoo160/src/purchase-workflow/purchase_landed_cost/views/purchase_cost_distribution_line_expense_view.xml
	36. /opt/sources/odoo160/src/purchase-workflow/purchase_landed_cost/views/purchase_expense_type_view.xml