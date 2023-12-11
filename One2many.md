>[[Campos relacionales|Back]]

Tags: 
Related: 

___

# One2many

## **Descripcion**

A One2many field allows you to link multiple records from one model to another. It is often used when you have a hierarchical or parent-child relationship between two entities. The "one" side usually represents the parent, and the "many" side represents the related child records.

## **Sintaxis:**

```python
field_name = fields.One2many('related.model', 'inverse_field', string='Field Label', [optional_parameters])`
```

- `field_name`: El nombre del campo en el modelo actual. (One)
- `'related.model'`: El nombre del modelo con el que se establecerá la relación (Many)
- [[Inverse field|inverse_field]]: The name of the inverse field in the related model.
- `string='Field Label'`: An optional label for the field that will be displayed in the user interface.
- [[#^f968d4|[optional_parameters]]]: Additional parameters such as `context` or `domain` for customization.
## **Ejemplos:**

### Ejemplo 1

```python
class ParentModel(models.Model):     _name = 'parent.model'     name = fields.Char(string='Parent Name')  class ChildModel(models.Model):     _name = 'child.model'     parent_ids = fields.One2many('parent.model', 'inverse_field', string='Children')
```

In this example, the one2many relationship is established between the `parent.model` and `child.model`. Each parent can have multiple children, and the field in the child model is labeled 'Children.'

### Ejemplo 2

Suppose we have two models, `Project` and `Task`, and we want to create a one-to-many relationship from `Project` to `Task`:

```python
class Project(models.Model):
    _name = 'project.project'
    name = fields.Char(string='Project Name')
    tasks = fields.One2many('project.task', 'project_id', string='Tasks')

class Task(models.Model):
    _name = 'project.task'
    name = fields.Char(string='Task Name')
    project_id = fields.Many2one('project.project', string='Project')
```

In this example, each project can have multiple tasks, and the one2many relationship is established through the 'project_id' field in the `project.task` model.

## Optional Parameters

^f968d4

- **comodel_name**:
	   name of the target model
    
- **inverse_name**:
	  name of the inverse `Many2one` field in `comodel_name`
    
- **domain**:
	  an optional domain to set on candidate values on the client side (domain or string)
    
- **context**:
	  an optional context to use on the client side when handling that field
    
- **auto_join**:
	   whether JOINs are generated upon search through that field (default: `False`)
    
- **limit**:
	  optional limit to use upon read
