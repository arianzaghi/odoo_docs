>[[ORM Methods|Back]]

Tags: #metodo

## Overview

This Odoo method is used to count the number of records in a model that match a given domain

```
record_count = self.env['your.model'].search_count(domain)`
```

## Example usage

Suppose you have a model named `my.model` with a field named `name`, and you want to count the records where the name is 'John':

pythonCopy code

```
john_count = self.env['my.model'].search_count([('name', '=', 'John')])`
```

In this example, `john_count` will hold the count of records in the `my.model` where the name is 'John'.