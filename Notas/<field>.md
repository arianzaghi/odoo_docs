> [[Etiquetas XML|Back]]

Tags: #xml
Links: 
# XML Tag "field" Guide

## 1. Introduction

The `<field>` tag is a fundamental element in XML used to define fields within a document. It is commonly employed for structuring data in various domains.

## 2. Syntax

The basic syntax of the `<field>` tag is `<field>value</field>`. It encapsulates the data or content associated with a specific field.

## 3. Attributes

The `<field>` tag may have attributes to provide additional information. Common attributes include:

- `name` (mandatory) [`Char`](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/orm.html#odoo.fields.Char "odoo.fields.Char")
    
    Only useful as a mnemonic/description of the view when looking for one in a list of some sort.
    
- `model` [`Char`](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/orm.html#odoo.fields.Char "odoo.fields.Char")
    
    The model linked to the view, if applicable.
    
- `priority` [`Integer`](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/orm.html#odoo.fields.Integer "odoo.fields.Integer")
    
    When a view is requested by `(model, type)`, the view matching the model and the type, with the lowest priority will be returned (it is the default view).
    
    It also defines the order of views application during [view inheritance](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/views.html#reference-views-inheritance).
    
- `groups_id` [`Many2many`](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/orm.html#odoo.fields.Many2many "odoo.fields.Many2many") -> `odoo.addons.base.models.res_users.Groups`
    
    The groups allowed to use/access the current view.
    
    If the view extends an existing view, the extension will only be applied for a given user if the user has access to the provided `groups_id`.
    
- `arch` [`Text`](https://www.odoo.com/documentation/16.0/es/developer/reference/backend/orm.html#odoo.fields.Text "odoo.fields.Text")
    
    The description of the view layout.

## 4. Example Usage

In a hypothetical XML document for a customer database, the `<field>` tag could be employed as follows:


```xml
<customer>
	<field name="firstName">John</field>
	<field name="lastName">Doe</field>
	<field name="age" type="integer">30</field>
</customer>
```

## 5. Domain-specific Considerations

When using `<field>` in a specific domain, tailor the attributes and content accordingly. For example, in a financial domain:


```xml
<transaction>
	<field name="transactionType">purchase</field>
	<field name="amount" type="decimal">150.50</field>
	<field name="currency">USD</field
</transaction>
```