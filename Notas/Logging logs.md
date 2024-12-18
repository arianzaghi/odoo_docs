> [[Back]]

Tags: 
Status: 
Related: 

___

# Logging logs

```python
import logging  
_logger = logging.getLogger(__name__)

_logger.info(f'Created {len(vals_list)} calculation records.')
_logger.warning(f'Created {len(vals_list)} calculation records.')
_logger.error(f'Created {len(vals_list)} calculation records.')
```