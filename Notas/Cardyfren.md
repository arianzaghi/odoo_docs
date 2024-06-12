> [[Clientes]]

Tags: 
Status: 
Related: 

___

# Cardyfren

## Client Mirror

1. Existen 2 lineas para `addons-standar` (eliminamos la que es `estandar`)
2. Ponemos `ops-client` antes que `addons-standar`
3. Hacemos pull en `ops-client` (no funciona bien el client)

**Config para cardydren**
``` 
addons_path =  
    /opt/sources/odoo120/src/addons-custom/cardyfren,  
    /opt/sources/odoo120/src/ops-client,  
    /opt/sources/odoo120/src/addons-standard,  
    /opt/sources/odoo120/src/core/addons,  
    /opt/sources/odoo120/src/enterprise,  
    /opt/sources/odoo120/src/account-analytic,  
    /opt/sources/odoo120/src/account-closing,  
    /opt/sources/odoo120/src/account-financial-reporting,  
    /opt/sources/odoo120/src/account-financial-tools,  
    /opt/sources/odoo120/src/account-fiscal-rule,  
    /opt/sources/odoo120/src/account-invoice-reporting,  
    /opt/sources/odoo120/src/account-invoicing,  
    /opt/sources/odoo120/src/account-payment,  
    /opt/sources/odoo120/src/bank-payment,  
    /opt/sources/odoo120/src/bank-statement-import,  
    /opt/sources/odoo120/src/bank-statement-reconcile,  
    /opt/sources/odoo120/src/business-requirement,  
    /opt/sources/odoo120/src/carrier-delivery,  
    /opt/sources/odoo120/src/commission,  
    /opt/sources/odoo120/src/community-data-files,  
    /opt/sources/odoo120/src/connector,  
    /opt/sources/odoo120/src/contract,  
    /opt/sources/odoo120/src/credit-control,  
    /opt/sources/odoo120/src/crm,  
    /opt/sources/odoo120/src/e-commerce,  
    /opt/sources/odoo120/src/edi,  
    /opt/sources/odoo120/src/event,  
    /opt/sources/odoo120/src/hr,  
    /opt/sources/odoo120/src/hr-timesheet,  
    /opt/sources/odoo120/src/knowledge,  
    /opt/sources/odoo120/src/l10n-spain,  
    /opt/sources/odoo120/src/management-system,  
    /opt/sources/odoo120/src/manufacture,  
    /opt/sources/odoo120/src/manufacture-reporting,  
    /opt/sources/odoo120/src/margin-analysis,  
    /opt/sources/odoo120/src/mis-builder,  
    /opt/sources/odoo120/src/multi-company,  
    /opt/sources/odoo120/src/partner-contact,  
    /opt/sources/odoo120/src/pos,  
    /opt/sources/odoo120/src/product-attribute,  
    /opt/sources/odoo120/src/product-kitting,  
    /opt/sources/odoo120/src/product-variant,  
    /opt/sources/odoo120/src/project,  
    /opt/sources/odoo120/src/project-reporting,  
    /opt/sources/odoo120/src/purchase-reporting,  
    /opt/sources/odoo120/src/purchase-workflow,  
    /opt/sources/odoo120/src/queue,  
    /opt/sources/odoo120/src/report-print-send,  
    /opt/sources/odoo120/src/reporting-engine,  
    /opt/sources/odoo120/src/rma,  
    /opt/sources/odoo120/src/sale-reporting,  
    /opt/sources/odoo120/src/sale-workflow,  
    /opt/sources/odoo120/src/server-tools,  
    /opt/sources/odoo120/src/server-ux,  
    /opt/sources/odoo120/src/social,  
    /opt/sources/odoo120/src/stock-logistics-barcode,  
    /opt/sources/odoo120/src/stock-logistics-reporting,  
    /opt/sources/odoo120/src/stock-logistics-tracking,  
    /opt/sources/odoo120/src/stock-logistics-transport,  
    /opt/sources/odoo120/src/stock-logistics-warehouse,  
    /opt/sources/odoo120/src/stock-logistics-workflow,  
    /opt/sources/odoo120/src/web,  
    /opt/sources/odoo120/src/webkit-tools,  
    /opt/sources/odoo120/src/website,  
    /opt/sources/odoo120/src/addons-external
```