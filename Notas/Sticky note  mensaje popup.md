> [[Wizards]]

Tags: 
Status: 
Related: 

___

# Sticky note  mensaje popup

```python
return {  
    'type': 'ir.actions.client',  
    'tag': 'display_notification',  
    'params': {  
        'title': 'Cron Scheduled',  
        'message': f'A cron job has been scheduled for {today_at_4am.strftime("%Y-%m-%d %H:%M:%S")}',  
        'sticky': False,  
    }  
}
```