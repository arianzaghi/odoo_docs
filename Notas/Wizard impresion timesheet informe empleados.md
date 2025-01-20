> [[Wizards]]

Tags: 
Status: 
Related: 

___

# Wizard impresion timesheet informe empleados

```python
class PntEmployeeTimeshiftWizard(models.TransientModel):  
    _name = 'pnt.employee.timeshift.wizard'  
    _description = 'Employee Timeshift Wizard'  
  
    def _get_available_months_in_analytic_lines(self):  
        """  
        Devuelve la lista de meses disponibles en las líneas analíticas de los empleados seleccionados.        """        months = list(set(x.strftime('%B') for x in self.env['account.analytic.line'].search([]).mapped('date')))  
        months.sort(key=lambda m: list(calendar.month_name).index(m))  
        selection_data = [(month, month) for month in months]  
        return selection_data  
  
    def _get_available_years_in_analytic_lines(self):  
        """  
        Devuelve la lista de años disponibles en las líneas analíticas de los empleados seleccionados.        """        years = list(set(x.strftime('%Y') for x in self.env['account.analytic.line'].search([]).mapped('date')))  
        years.sort()  
        selection_data = [(year, year) for year in years]  
        return selection_data  
  
    pnt_employee_ids = fields.Many2many(comodel_name='hr.employee', string='Employees', )  
    pnt_apply_to_all = fields.Boolean(string='Select all employees', default=False, )  
    pnt_month = fields.Selection(  
        selection=_get_available_months_in_analytic_lines,  
        string='Month Selection',  
        required=True,  
    )  
    pnt_year = fields.Selection(  
        selection=_get_available_years_in_analytic_lines,  
        string='Year Selection',  
        required=True,  
    )  
  
    def print_report(self):  
        report = self.env["ir.actions.report"]._get_report(  
            "report_pnt.pnt_timeshift_report_action"  
        )  
        return report.report_action(self)
```