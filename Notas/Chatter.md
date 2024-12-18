> [[031 - Elementos de Interfaz]]

Tags: 
Status: 
Related: 

___

# Chatter

![[Pasted image 20241212171645.png]] ^9aa17f

```python
<div class="oe_chatter">
	<field name="message_follower_ids" groups="base.group_user"/>
	<field name="activity_ids"/>
	<field name="message_ids"/>
</div>
```

> [!IMPORTANT] Importante
> El modelo en el que insertemos el `chatter` debe de heredar de:
> ```python
> _inherit = ['mail.thread', 'mail.activity.mixin']
> ```

## Actividades con chatter
- [[Ocultar chatter para un grupo]]
- [[Mostrar mensaje en chatter después de un evento]]