> [[Github]]

Tags: 
Status: 
Related: 

___
# Crear una rama nueva a partir de una plantila sin historial

```sh
# Creamos rama nueva sin historial
git checkout --orphan {{limpia}}  
# Borramos todos los ficheros del github

git rm -rf .

# Descargamos y extraemos contenido de 17.0_template en nuestro repo  
git add .

git commit -m "Inicio de rama limpia"  
git push -u origin limpia
```