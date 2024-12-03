> [[Back]]

Tags: 
Status: 
Related: 

___

# Contextos

> Los contextos sirven para pasar valores temporales de un modelo a otro.
> Para poder saber desde qué botón se está llamando a una función, o qué valores predeterminados usar cuando vamos a crear un registro de otro modelo en un popup o en su propio form. 


```python
@api.model  
def default_get(self, fields):  
    res = super(PntCreateCalcsWizard, self).default_get(fields)  
    return res
```
> Con este metodo puedo ver los parametros que se pasan por contexto en `self.env.context`

[[Contexto por botón a un record]]
[[Pasar contexto a un metodo]]
[[Llamar un método con contexto]]