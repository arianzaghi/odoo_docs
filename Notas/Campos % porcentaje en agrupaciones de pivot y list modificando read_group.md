> [[Back]]

Tags: 
Status: 
Related: 

___

# Campos % porcentaje en agrupaciones de pivot y list modificando read_group


> Cuando tenemos un modelo que guarda registros diarios por empleado y tiene algún campo %, al agrupar en la vista `list` o `pivot` los % se suman y pueden dar valores erroneos.

> [!INFO] Heredamos Read Groups
> Llamando a super en el read groups podemos ver todos los campos que se estan renderizando en pantalla, y podemos asignar un nuevo valor a los campos % en base a la suma (ya realizada por odoo) de los campos sobre los que se calcula el % (numerador y denominador)

### Descripcion de campos y sus formulas
> Aqui definimos nuestros campos %

```python
    def _get_percentage_field_configs(self) -> Dict[str, Dict[str, str]]:
        """
        Definimos los campos de tipo porcentaje y su calculo
        indicando numerador y denominador
        Returns:
            dict: Configuration mapping for percentage fields
        """
        return {
            "pnt_employment_percentage": {
                "numerator": "pnt_employee_attendance_hours",
                "denominator": "pnt_work_entry_theoretical_hours",
            },
            "pnt_performance_percentage": {
                "numerator": "pnt_timesheet_invested_hours",
                "denominator": "pnt_employee_attendance_hours",
            },
            "pnt_productivity_percentage": {
                "numerator": "pnt_timesheet_invoiced_hours",
                "denominator": "pnt_employee_attendance_hours",
            },
        }
```
### Bloque de calculo y herencia read_groups
> Este bloque de python se copia tal cual
```python
    @api.model
    def read_group(
        self,
        domain: List,
        fields: List[str],
        groupby: List[str],
        offset: int = 0,
        limit: int = None,
        orderby: bool = False,
        lazy: bool = True,
    ) -> List[Dict[str, Any]]:
        """
        Heredamos read_group para asegurar que los totales de los campos
        de porcentaje se calculen en base a la suma de sus numeradores
        y denominadores, en lugar de promediar los porcentajes individuales.
        """
        # Call the original read_group to get the default aggregated data
        res = super().read_group(
            domain,
            fields,
            groupby,
            offset=offset,
            limit=limit,
            orderby=orderby,
            lazy=lazy,
        )

        # Process percentage fields for grouped data
        percentage_field_configs = self._get_percentage_field_configs()

        for line in res:
            # Only process group lines (not individual records)
            if "__domain" in line:
                self._compute_group_percentages(line, fields, percentage_field_configs)

        return res

    def _compute_group_percentages(
        self,
        line: Dict[str, Any],
        fields: List[str],
        configs: Dict[str, Dict[str, str]],
    ) -> None:
        """
        Si el campo de porcentaje está en los campos solicitados,
        calcular el porcentaje usando los valores agregados de numerador y denominador.
        Args:
            line: Group line data to update
            fields: Requested fields list
            configs: Percentage field configurations
        """
        for percentage_field, config in configs.items():
            if (
                percentage_field in fields
                or percentage_field + ":avg" in fields
                or percentage_field + ":sum" in fields
            ):  # noqa: E501
                numerator_value = line.get(config["numerator"], 0.0)
                denominator_value = line.get(config["denominator"], 0.0)

                if denominator_value > 0:
                    percentage = (numerator_value / denominator_value) * 100
                else:
                    percentage = 0.0

                line[percentage_field] = percentage
```