> [[Back]]

Tags: 
Status: 
Related: 

___

# Configurar Apple Pay y Google Pay en Redsys

> Tenemos que descomentar una linea del modulo payment_redsys


`payment_redsys>payment_provider`
```python
def _prepare_merchant_parameters(self, tx_values):
	"Ds_Merchant_Paymethods": self.redsys_pay_method or "T",
```

Lo quitamos mediante un hooks y automáticamente aparecen los nuevos métodos de pago.


> [!WARNING] AVISO
> Apple Pay solo saldrá en dispositivos Apple

[Ezedichi v17](https://github.com/puntsistemes/ezedichi_odoo/pull/55)