> [[Odoo Traducciones|Back]]

Tags: 
Status: 
Related: [[Odoo Traducciones]]

___

# Traducir campo del core

1. Creamos el módulo `i18n_pnt` a partir de la carpeta `dev-tools/scaffolding`

![[Pasted image 20240523104011.png]]

1. Pegamos en el fichero `*.po` las traducciones del modulo original que queremos sobreescribir

```po
# Translation of Odoo Server.  
msgid ""  
msgstr ""  
"Project-Id-Version: Odoo Server 16.0+e\n"  
"Report-Msgid-Bugs-To: \n"  
"POT-Creation-Date: 2024-02-15 10:07+0000\n"  
"PO-Revision-Date: 2024-02-15 10:07+0000\n"  
"Last-Translator: \n"  
"Language-Team: \n"  
"MIME-Version: 1.0\n"  
"Content-Type: text/plain; charset=UTF-8\n"  
"Content-Transfer-Encoding: \n"  
"Plural-Forms: \n"

#. module: hr  
#: model:ir.model.fields,field_description:hr.field_hr_department__manager_id  
#: model:ir.model.fields,field_description:hr.field_hr_employee__parent_id  
#: model:ir.model.fields,field_description:hr.field_hr_employee_base__parent_id  
#: model:ir.model.fields,field_description:hr.field_hr_employee_public__parent_id  
#: model:ir.model.fields,field_description:hr.field_res_users__employee_parent_id  
#: model:ir.model.fields.selection,name:hr.selection__hr_plan_activity_type__responsible__manager  
#: model_terms:ir.ui.view,arch_db:hr.hr_employee_public_view_search  
#: model_terms:ir.ui.view,arch_db:hr.view_employee_filter  
msgid "Manager"  
msgstr "NUEVA TRADUCCION"
```

4. Añadimos en el depends el módulo que vamos a re-traducir (`hr`)
```python
{  
    "name": "Translations for third party modules",  
    "version": "16.0.1.0.0",  
    "category": "Customizations",  
    "website": "https://www.puntsistemes.es",  
    "author": "Punt Sistemes",  
    "summary": "Translations for third party modules",  
    "license": "AGPL-3",  
    "application": False,  
    "installable": True,  
    "depends": [  
        "hr",  
    ],  
}
```

>**Relatos de Gonzalo**
>Te cuento como solucioné lo de la traducción... Copié y pegué el módulo de scafolding (eso lo hicimos juntos), actualicé el nuevo módulo i18n y me descargué la traducción del módulo de la OCA, lo hice en el PO Edit, y copié y pegué el contenido del bloc de notas del PO en el archivo es.po del módulo creado para este modelo de la OCA.


## Ejemplos

### [Educonsul v16](https://github.com/puntsistemes/educonsul_odoo/commit/96972f65c1326a9619fdb87485f9487bc1d8e5ee#diff-2a0b142bc4dd1804422b2207289b191126ef7e52e48421d0feb43c6c2c93c69f)