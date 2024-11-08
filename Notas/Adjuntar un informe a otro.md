> [[Impresion de informes]]

Tags: 
Status: 
Related: 

___

# Imprimir y adjuntar un informe a otro
## Resumen de la tarea

Al imprimir un informe de tipo factura, queremos que también se impriman y adjunten todos los albaranes asociados a esa factura

**Tareas principales**
- Localizar albaranes relacionados con la factura
- Imprimir los albaranes encontrados
- Adjuntar los albaranes a la factura

## Programación

```python
from odoo import models, _
from io import BytesIO


class IrActionsReport(models.Model):
    _inherit = "ir.actions.report"
    
    def _render_qweb_pdf(self, report_ref, res_ids=None, data=None):
        res = super()._render_qweb_pdf(report_ref, res_ids=res_ids, data=None)
        
        CLIENT_FORMATS = [
            "MODEL.report_to_motnitor_1",
            "MODEL.report_to_motnitor_2",
        ]
        
        if report_ref in CLIENT_FORMATS and res_ids:
            pickings = self.env["account.move"].browse(res_ids).mapped('picking_ids')
            if pickings:
                combined_pdf_content = self._get_combined_pdf(res, pickings)
                streams = [BytesIO(res[0]), BytesIO(combined_pdf_content)]
                merge = self._merge_pdfs(streams)
                return merge.getvalue(), "pdf"
        return res
        
    def _get_combined_pdf(self, invoice_pdf_content, pickings):
        output_stream = BytesIO()
        
        picking_report_action = self.env.ref('report_pnt.pnt_action_report_delivery_invoice')
        
        report_ref  =  "report_pnt.pnt_report_deliveryslip_invoice"
        
        res_ids = pickings.ids
        picking_pdf_content, _ = picking_report_action._render_qweb_pdf(report_ref, res_ids=res_ids, data=None)
        output_stream.write(picking_pdf_content)
        
        return output_stream.getvalue()
```

## Ejemplos 

### [Anton v16](https://github.com/puntsistemes/anton_odoo/commit/787e56e60e86bdc175ebc113448a36b29c0ab9a8#diff-71204097483a0ed38ebc82c6d57437d51d9348759233b3cc757749298eaaef07)

```python
from odoo import models, _
from io import BytesIO


class IrActionsReport(models.Model):
    _inherit = "ir.actions.report"
    
    def _render_qweb_pdf(self, report_ref, res_ids=None, data=None):
        res = super()._render_qweb_pdf(report_ref, res_ids=res_ids, data=None)
        
        anton_invoice = [
            "report_pnt.report_invoice_anton_new_pnt",
            "report_pnt.report_invoice_anton_aparatologia_pnt",
        ]
        
        if report_ref in anton_invoice and res_ids:
            pickings = self.env["account.move"].browse(res_ids).mapped('picking_ids')
            if pickings:
                combined_pdf_content = self._get_combined_pdf(res, pickings)
                streams = [BytesIO(res[0]), BytesIO(combined_pdf_content)]
                merge = self._merge_pdfs(streams)
                return merge.getvalue(), "pdf"
        return res
        
    def _get_combined_pdf(self, invoice_pdf_content, pickings):
        output_stream = BytesIO()
        
        picking_report_action = self.env.ref('report_pnt.pnt_action_report_delivery_invoice')
        
        report_ref  =  "report_pnt.pnt_report_deliveryslip_invoice"
        
        res_ids = pickings.ids
        picking_pdf_content, _ = picking_report_action._render_qweb_pdf(report_ref, res_ids=res_ids, data=None)
        output_stream.write(picking_pdf_content)
        
        return output_stream.getvalue()
```
