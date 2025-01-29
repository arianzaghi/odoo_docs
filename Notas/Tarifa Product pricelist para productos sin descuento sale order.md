> [[sale.order.line]]

Tags: 
Status: 
Related: [[sale.order.line]]

___

# Product pricelist para productos sin descuento

> Anton v16 HU61560-Modificacion_Tarifas_de_venta
##  Resumen de Requisitos

1. **Campo "No Descuento" en Tarifas:**
    - Agregar un campo booleano en `product.pricelist`.
    - Solo una tarifa puede tener este campo activo.
2. **Restricciones de la Tarifa "No Descuento":**
    - Solo permite variantes (`product.product`).
    - Solo acepta precios fijos o descuentos (%).
    - Respeta cantidad mínima y fechas de validez.
3. **Lógica de Precios en Documentos de Venta:**
    - Buscar primero en la tarifa "No Descuento".
    - Si el producto está en la tarifa, usar su precio o descuento.
    - Si no está, aplicar la tarifa estándar del documento de venta.

## Pricelist
```python
class ProductPricelist(models.Model):  
    _inherit = "product.pricelist"  
  
    pnt_no_discount_pricelist = fields.Boolean(  
        string="No Discount Pricelist",  
    )  
  
    @api.constrains("pnt_no_discount_pricelist")  
    def _check_pnt_portal_particular_default(self):  
        if self.pnt_no_discount_pricelist:  
            checked_bool = self.search(  
                [("id", "!=", self.id), ("pnt_no_discount_pricelist", "=", True)], limit=1  
            )  
            if checked_bool:  
                raise ValidationError(  
                    _(  
                        "There's already one pnt_portal_particular_default is checked. Reference : %s"  
                    )  
                    % checked_bool.name  
                )
```

## PricelistItem
```python
class ProductPricelistItem(models.Model):  
    _inherit = "product.pricelist.item"

@api.constrains('applied_on', 'compute_price')  
def _check_no_discount_constraints(self):  
    for record in self:  
        if record.pricelist_id.pnt_no_discount_pricelist:  
            if record.applied_on != '0_product_variant':  
                raise ValidationError("Only variants can be added in the 'No Discount' pricelist.")  
            if record.compute_price not in ['fixed', 'percentage']:  
                raise ValidationError("Only fixed prices or discounts can be used in the 'No Discount' pricelist.")
```

## Sale order
```python
@api.onchange('product_id')  
def _onchange_product_id(self):  
    if not self.product_id:  
        return  
  
    no_discount_pricelist = self.env['product.pricelist'].search([('pnt_no_discount_pricelist', '=', True)], limit=1)  
    price = no_discount_pricelist._get_products_price(self.product_id, self.product_uom_qty) if no_discount_pricelist else False  
  
    if price:  
        self.price_unit = price.get(self.product_id.id)  
        return  
  
    original_pricelist = self.order_id.pricelist_id  
    original_pricelist_price = original_pricelist._get_products_price(self.product_id, self.product_uom_qty) if original_pricelist else False  
  
    self.price_unit = original_pricelist_price.get(self.product_id.id) if original_pricelist_price else self.product_id.list_price
```

```xml
<record id="pnt_product_pricelist_form_view" model="ir.ui.view">  
    <field name="model">product.pricelist</field>  
    <field name="inherit_id" ref="product.product_pricelist_view"/>  
    <field name="arch" type="xml">  
        <field name="active" position="after">  
            <field name="pnt_no_discount_pricelist"/>  
        </field>  
    </field>  
</record>
```