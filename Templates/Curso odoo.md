<%*
	let title = tp.file.title
	if (title.startsWith("Untitled")){
		title = await tp.system.prompt("Title");
		await tp.file.rename(title);
	}
%>> [[curso_odoo]]

Tags: 
Status: 
Related: 

Video: 
Minuto:

___

# <%*tR += title %>

