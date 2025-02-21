> [[090  - Servidor gestion]]

Tags: 
Status: 
Related: [[Dev-tools]]

___

# Plantillas para crear docker en clientes

Las podemos encontrar dentro de github con el nombre:

> `template-16.0_odoo`

[[Crear una rama nueva a partir de una plantila sin historial]]

Una vez que encuentras las plantilla le das a crear nuevo repositorio

![[Pasted image 20240917084940.png]]
Luego lo nombras con el nombre del cliente_odoo
![[Pasted image 20240917085023.png]]

Y luego debes completar el fichero [excel](https://sistemespunt-my.sharepoint.com/:x:/r/personal/igallart_puntsistemes_es/_layouts/15/doc2.aspx?sourcedoc=%7B45196DD3-F24E-467E-A233-1F29F3CB24A1%7D&file=clientes_github_actions.xlsx&action=default&mobileredirect=true&wdOrigin=TEAMS-WEB.p2p_ns.rwc&wdExp=TEAMS-TREATMENT&wdhostclicktime=1717513048517&web=1&ovuser=81412df1-9a6d-49c9-aca3-611b6f979c0b%2CGCrosio%40puntsistemes.es&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiIxNDE1LzI0MDgwMjEyMDExIiwiSGFzRmVkZXJhdGVkVXNlciI6ZmFsc2V9) para que Isaac o Juanvi completen la configuración del github/actions.

Los datos para el excel lo puedes conseguir conectandote al servidor y lanzando el comando "**pg_lsclusters**" y con eso tienes toda la información necesaria dentro del servidor y para completar el bash_aliases y el config dentro de source/dev-tools lanzas un commit "ADD: [nombre cliente]" y así dejas todo actualizado