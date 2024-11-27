> [[Vista List o Tree - Listado]]

Tags: #xml
Status: 
Related: 

___

# Tree view groupby

>Agrupamos los resultados de la búsqueda en la vista List
```python
<group string="Group By" name="groupby">  
    <filter name="user_id_groupby" string ="User" context="{'group_by': 'user_id'}"/>  
    <filter name="date_groupby" string="Date" context="{'group_by': 'date'}"/>  
</group>
```

