> [[Vista Pivot]]

Tags: 
Status: 
Related: 

___

# SQL Para vista pivot

> Modelo de odoo que no queda guardado en bbdd `(auto = False)` y utilizamos para crear vistas con datos de diferentes modelos. Los datos se cargan y representan al momento.

## Punt Sistemes 
https://github.com/puntsistemes/punt-sistemes_odoo/pull/153

```python
from odoo import models, fields, api, tools  
  
class PntWorkControlReport(models.Model):  
    _name = "pnt.milestone.report"  
    _auto = False  
  
    pnt_project_id = fields.Many2one("project.project", string="Project", readonly=True)  
    pnt_partner_id = fields.Many2one("res.partner", string="Partner", readonly=True)  
    pnt_product_template_id = fields.Many2one("product.template", string="Milestone", readonly=True)  
    pnt_sale_order_id = fields.Many2one("sale.order", string="Sale Order", readonly=True)  
    pnt_deadline = fields.Date(string="Deadline", readonly=True)  
    pnt_price = fields.Float(string="Price", readonly=True)  
    pnt_employee_id = fields.Many2one("hr.employee", string="Employee", readonly=True)  
    pnt_invoice_status = fields.Selection(  
        selection=[  
            ('to invoice', "To Invoice"),  
            ('no', "Nothing to Invoice"),  
        ],  
        string="Invoice Status", readonly=True)  
  
  
    def _query(self):  
        return """  
            SELECT                m.id AS id,                rp.id AS pnt_partner_id,                p.id AS pnt_project_id,                so.id AS pnt_sale_order_id,                pt.id AS pnt_product_template_id,                m.deadline AS pnt_deadline,                sl.price_subtotal AS pnt_price,                sl.invoice_status AS pnt_invoice_status,                em.id AS pnt_employee_id            FROM project_milestone m            INNER JOIN project_project p ON m.project_id = p.id            INNER JOIN sale_order_line sl ON m.sale_line_id = sl.id            LEFT JOIN hr_employee em ON p.pnt_project_manager_id = em.user_id            LEFT JOIN product_product pr ON sl.product_id = pr.id            LEFT JOIN product_template pt ON pr.product_tmpl_id = pt.id            LEFT JOIN sale_order so ON sl.order_id = so.id            LEFT JOIN res_partner rp ON so.partner_id = rp.id            WHERE                sl.invoice_status IN ('no', 'to invoice')                AND so.state = 'sale'        """  
    @property  
    def _table_query(self):  
        return self._query()
```
## Palacio de Congresos
https://github.com/puntsistemes/palacio-congresos_odoo/pull/138

```python
from odoo import models, fields, api, tools


class PntDailyExtraHourCalc(models.Model):
    _name = "pnt.extra.hour.report"
    _auto = False  # Es una vista SQL

    pnt_origin_id = fields.Many2one("pnt.daily.extra.hour.calc", string="Origin", readonly=True)
    pnt_day = fields.Date(string="Date", readonly=True)
    pnt_employee_id = fields.Many2one("hr.employee", string="Employee", readonly=True)
    pnt_value = fields.Float(string="Hours", readonly=True)
    # Tipo de horas extras o ausencias
    pnt_type = fields.Selection([
        ('pnt_01_max_workable_hours', "1. Maximum workable hours"),
        ('pnt_02_paid_hours_and_bonified', "2. Paid hours + bonification"),
        ('pnt_03_total_hours', "3. Total hours"),
        ('pnt_04_total_bonified_hours', "4. Total bonified hours"),
        ('pnt_05_balance', "5. Balance"),
        ('pnt_06_regular_schedule', "6. On site work"),
        ('pnt_07_remote_work', "7. Remote work"),
        ('pnt_08_free_disposal_days', "8. Free Disposal Days"),
        ('pnt_09_external_visit', "9. External visit"),
        ('pnt_10_paid_sickness', "10. Paid sickness"),
        ('pnt_11_extra_hour', "11. Extra hour count"),
        ('pnt_12_festive_hour', "12. Festive hour count"),
        ('pnt_13_night_hour', "13. Night hour count"),
        ('pnt_14_extra_festive_hour', "14. Extra festive hour count"),
        ('pnt_15_extra_night_hour', "15. Extra night hour count"),
        ('pnt_16_festive_night_hour', "16. Festive night hour"),
        ('pnt_17_extra_festive_night_hour', "17. Extra festive night hour"),
        ('pnt_18_bon_extra_hour', "18. Bonified extra hour"),
        ('pnt_19_bon_festive_hour', "19. Bonified festive hour"),
        ('pnt_20_bon_night_hour', "20. Bonified night hour"),
        ('pnt_21_bon_extra_festive_hour', "21. Bonified extra festive hour"),
        ('pnt_22_bon_extra_night_hour', "22. Bonified extra night hour"),
        ('pnt_23_bon_festive_night_hour', "23. Bonified festive night hour"),
        ('pnt_24_bon_extra_festive_night_hour', "24. Bonified extra festive night hour"),
        ('pnt_25_holidays', "25. Holidays"),
    ], string="Extra hours detail", readonly=True)



    def _query(self):
        return """
            SELECT
                row_number() OVER () AS id,
                p.pnt_day AS pnt_day,
                p.pnt_employee_id AS pnt_employee_id,
                p.id AS pnt_origin_id,
                unnest(array[
                    'pnt_01_max_workable_hours', 'pnt_02_paid_hours_and_bonified',
                    'pnt_03_total_hours', 'pnt_04_total_bonified_hours', 'pnt_05_balance',
                    'pnt_06_regular_schedule', 'pnt_07_remote_work', 'pnt_08_free_disposal_days',
                    'pnt_09_external_visit', 'pnt_10_paid_sickness', 'pnt_11_extra_hour',
                    'pnt_12_festive_hour', 'pnt_13_night_hour', 'pnt_14_extra_festive_hour',
                    'pnt_15_extra_night_hour', 'pnt_16_festive_night_hour', 'pnt_17_extra_festive_night_hour',
                    'pnt_18_bon_extra_hour', 'pnt_19_bon_festive_hour', 'pnt_20_bon_night_hour',
                    'pnt_21_bon_extra_festive_hour', 'pnt_22_bon_extra_night_hour',
                    'pnt_23_bon_festive_night_hour', 'pnt_24_bon_extra_festive_night_hour',
                    'pnt_25_holidays'
                ]) AS pnt_type,
                unnest(array[
                    COALESCE(p.pnt_max_workable_hours, 0),
                    COALESCE(p.pnt_paid_hours_and_bonified, 0),
                    COALESCE(p.pnt_total_hours, 0),
                    COALESCE(p.pnt_total_bonified_hours, 0),
                    COALESCE(p.pnt_balance, 0),
                    COALESCE(p.pnt_regular_schedule, 0),
                    COALESCE(p.pnt_remote_work, 0),
                    COALESCE(p.pnt_free_disposal_days, 0),
                    COALESCE(p.pnt_external_visit, 0),
                    COALESCE(p.pnt_paid_sickness, 0),
                    COALESCE(p.pnt_extra_hour, 0),
                    COALESCE(p.pnt_festive_hour, 0),
                    COALESCE(p.pnt_night_hour, 0),
                    COALESCE(p.pnt_extra_festive_hour, 0),
                    COALESCE(p.pnt_extra_night_hour, 0),
                    COALESCE(p.pnt_festive_night_hour, 0),
                    COALESCE(p.pnt_extra_festive_night_hour, 0),
                    COALESCE(p.pnt_bon_extra_hour, 0),
                    COALESCE(p.pnt_bon_festive_hour, 0),
                    COALESCE(p.pnt_bon_night_hour, 0),
                    COALESCE(p.pnt_bon_extra_festive_hour, 0),
                    COALESCE(p.pnt_bon_extra_night_hour, 0),
                    COALESCE(p.pnt_bon_festive_night_hour, 0),
                    COALESCE(p.pnt_bon_extra_festive_night_hour, 0),
                    COALESCE(p.pnt_holidays, 0)
                ]) AS pnt_value
            FROM pnt_daily_extra_hour_calc p
        """

    @property
    def _table_query(self):
        return self._query()
```