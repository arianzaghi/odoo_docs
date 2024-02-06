>[[Campos relacionales|Back]]

Tags: 
Related: 

___

## **Description**

En Odoo, las relaciones "many2many" te permiten establecer una conexión de muchos a muchos entre dos modelos. Esto implica que varios registros en un modelo pueden estar asociados con varios registros en otro modelo.

## **Syntax:**

```python
field_name = fields.Many2many(
	'related.model',
	'relation_table',
	'column1',
	'column2',
	string='Field Label',
	[optional_parameters]
)
```

- `field_name`: El nombre del campo en el modelo actual. (Many)
- `'related.model'`: El nombre del modelo con el que se establecerá la relación. (Many)
- `'relation_table'`: El nombre de la tabla que almacenará la relación many-to-many.
- `'column1'` y `'column2'`: Los nombres de las columnas en la tabla de relación que se vinculan a cada uno de los modelos.
- `string='Field Label'`: Una etiqueta opcional para el campo en la UI
- [[#^a48cf4|[optional_parameters]]]: Parámetros adicionales como `context` o `domain` para personalización.

## **Examples:**

### Example 1

```python
class Employee(models.Model):
    _name = 'hr.employee'
    name = fields.Char(string='Employee Name')
    
    projects = fields.Many2many(
	    'project.project',
	    'employee_project_rel',
	    'employee_id', 'project_id',
	    string='Projects'
	)
```

En este ejemplo, la relación many2many se establece entre los modelos `hr.employee` y `project.project`. Se crea una tabla adicional llamada `employee_project_rel` para almacenar la relación, y las columnas `employee_id` y `project_id` se vinculan a los respectivos modelos.

### Example 2

Supongamos que tenemos dos modelos, `Student` y `Course`, y queremos crear una relación de muchos a muchos:

```python
class Student(models.Model):
    _name = 'student.student'
    name = fields.Char(string='Student Name')
    courses = fields.Many2many(
	    'course.course',
	    'student_course_rel',
	    'student_id',
	    'course_id',
	    string='Courses'
	)

class Course(models.Model):
    _name = 'course.course'
    name = fields.Char(string='Course Name')
```

En este ejemplo, la relación many2many se establece entre los modelos `student.student` y `course.course`. La tabla adicional llamada `student_course_rel` almacena la relación many-to-many, y las columnas `student_id` y `course_id` se vinculan a los respectivos modelos.

## Optional Parameters

^a48cf4

- **relation:** El nombre de la tabla que almacenará la relación many-to-many. Obligatorio.
    
- **column1:** El nombre de la columna que se vincula al modelo actual en la tabla de relación. Obligatorio.
    
- **column2:** El nombre de la columna que se vincula al modelo relacionado en la tabla de relación. Obligatorio.
    
- **domain:** Un dominio opcional para filtrar los registros disponibles en el lado del cliente (dominio o cadena).
    
- **context (dict):** Un contexto opcional para usar en el lado del cliente al manejar ese campo.
    
- **limit (int):** Límite opcional para establecer en la cantidad de registros mostrados para esta relación.
    
- **order (str):** Una cadena que proporciona el orden predeterminado a utilizar para la relación.