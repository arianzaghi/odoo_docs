> [[Instalar módulos en odoo v17]]

Tags: 
Status: 
Related: [[OCA]]

___

# Instalación módulos OCA

## Modulos de remesas

`cd src/addons-custom/cliente/oca`

```sh
# Este es del que dependen todos los demas
ln -sf ../../bank-payment/account_payment_order .

ln -sf ../../bank-payment/account_banking_mandate .
ln -sf ../../bank-payment/account_banking_pain_base .
ln -sf ../../bank-payment/account_banking_sepa_credit_transfer .
ln -sf ../../bank-payment/account_banking_sepa_direct_debit .


ln -sf ../../l10n-spain/l10n_es_account_banking_sepa_fsdd .
```