> [[Cardyfren v12]]

Tags: 
Status: 
Related: 

___

# Script de módulos en Servidor Cardyfren


odoo@cardyfren:~/dev-tools_odoo/scripting$ python3 module_analyzer_stats.py

Cliente: Cardyfren
Versión de Odoo: 12.0

Total de módulos instalados: 285
Modulos core: 77 (27.02%)
Modulos enterprise: 38 (13.33%)

Modulos OCA: 153 (53.68%)

Modulos addons-external: 0 (0.00%)
Modulos addons-puntsistemes: 0 (0.00%)
Modulos addons-standard: 3 (1.05%)
Modulos addons-custom: 14 (4.91%)

Total de módulos a migrar/revisar: 170 (59.65%)
(addons-external, addons-puntsistemes, addons-standard, addons-custom)

Líneas de código python en addons-custom de 88 caracteres (no se cuentan commentarios ni líneas en blanco): 3129
Líneas de código xml en addons-custom de 88 caracteres (no se cuentan commentarios ni líneas en blanco): 1559

Total de métodos en addons-custom (def method): 393
Total de métodos que llaman a super() en addons-custom: 96
Total de campos en addons-custom (fields): 281

Modelos heredados en addons-custom: 56
account.account
account.analytic.account
account.followup.report
account.invoice
account.invoice.line
account.journal
account.move.line
account.payment
account.payment.order
account.register.payments
account.tax
account.voucher
base
delivery.carrier
force.done
hr.leave
ir.actions.report
ir.model
ir.ui.menu
ir.ui.view
mrp.bom
mrp.bom.line
mrp.production
prestashop.product
prestashop.product.template
prestashoperp.sync.now
product.attribute
product.category
product.product
product.supplierinfo
product.template
project.project
purchase.order
purchase.order.line
purchase.order.type
res.company
res.config.settings
res.groups
res.partner
res.users
sale.advance.payment.inv
sale.order
sale.order.line
sale.order.type
stock.location
stock.move
stock.move.line
stock.picking
stock.picking.type
stock.production.lot
stock.quant
stock.quantity.history
stock.rule
stock.warehouse
wk.order.mapping
wk.skeleton