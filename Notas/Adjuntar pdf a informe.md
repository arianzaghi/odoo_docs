> [[Impresion de informes]]

Tags: 
Status: 
Related: 

___

# Adjuntar pdf a informe

## Ejemplo 1

> [Coralim v16 - COA y security_sheet](https://github.com/puntsistemes/coralim_odoo/pull/61)


**Clase desde donde hacemos el attatchment**
```python
class IrActionsReport(models.Model):  
    _inherit = "ir.actions.report"  
```


**Procesamos cada uno de los informes que se van a imprimir**
```python
def _render_qweb_pdf(self, report_ref, res_ids=None, data=None):  
	res = super()._render_qweb_pdf(report_ref, res_ids=res_ids, data=data)  
	
	coralim_coa = [  
		"stock.report_deliveryslip",  
		"report_pnt.pnt_report_deliveryslip",  
		"report_pnt.repnt_packing_list"  
	]  
	
	if report_ref in coralim_coa and res_ids:  
		pickings = self.env["stock.picking"].browse(res_ids)  
		streams_coa = self.get_streams_coa(pickings)  
		streams_security_sheet = self.get_stream_security_sheet(pickings)  
		streams = [BytesIO(res[0])] + streams_coa + streams_security_sheet  
		
		merge = self._merge_pdfs(streams)  
		return merge.getvalue(), "pdf"  

	return res  
```

> [!Note] Nota
> En la lista de informes `coralim_coa` guardamos el nombre del [[Template de Invocación]] de nuestro informe

**Añadimos el informe del COA del modelo del lote**
```python
def get_streams_coa(self, pickings):  
	products = []  
	streams = []  
	for picking in pickings:  
		for line in picking.move_line_ids.filtered(lambda x: x.lot_id):  
			str_key = f"{line.product_id.product_tmpl_id.id}_{line.lot_id.id}"  
			if str_key not in products:  
				products.append(str_key)  
				stream = line.lot_id.message_main_attachment_id.filtered(  
					lambda x: x.name  
				)  
				if stream:  
					streams.append(BytesIO(stream[0].raw))  
	return streams  
```

**Añadimos la hoja de seguridad**
```python
def get_stream_security_sheet(self, pickings):  
        products = []  
        streams = []  
        for picking in pickings:  
            for line in picking.move_line_ids.filtered(  
                lambda x: x.product_id.product_tmpl_id not in products  
                          and x.product_id.product_tmpl_id.pnt_sector.pnt_print_security_sheet  
            ):  
                products.append(line.product_id.product_tmpl_id)  
                pnt_folder_id_security_sheet = (  
                    self.env["ir.config_parameter"]  
                    .sudo()  
                    .get_param("pnt_folder_id_security_sheet")  
                )  
                lang = picking.partner_id.pnt_documentation_lang or picking.partner_id.parent_id.pnt_documentation_lang  
                if not lang:  
                    raise UserError(  
                        _("Please set the document language of the partner %s")  
                        % picking.partner_id.name  
                    )  
                document = self.env["documents.document"].search(  
                    [  
                        ("res_id", "=", line.product_id.product_tmpl_id.id),  
                        ("res_model", "=", "product.template"),  
                        ("type", "=", "binary"),  
                        ("folder_id.id", "=", pnt_folder_id_security_sheet),  
                        ("name", "ilike", lang),  
                    ]  
                )  
                if document:  
                    streams.append(BytesIO(document[0].raw))  
        return streams
```