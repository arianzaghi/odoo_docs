> [[Back]]

Tags: 
Status: 
Related: 

___

# Imprimir un informe con contexto

En vez de usar un `ir.actions.report` usaremos un `ir.actions.server`

Hay que ocultar binding_model_id y binding_type para que no salgan los botones duplicados
```xml
    <!-- 2) Acción de informe vinculada al picking -->  
<!--    <record id="action_report_pnt_picking_label" model="ir.actions.report">-->  
<!--        <field name="name">Etiqueta de entrada</field>-->  
<!--        <field name="model">stock.picking</field>-->  
<!--        <field name="report_type">qweb-pdf</field>-->  
<!--        &lt;!&ndash; tu template QWeb principal &ndash;&gt;-->  
<!--        <field name="report_name">report_pnt.report_pnt_delivery_document_in</field>-->  
<!--        <field name="report_file">report_pnt.report_pnt_delivery_document_in</field>-->  
<!--        &lt;!&ndash; usa el paperformat que definimos arriba &ndash;&gt;-->  
<!--        <field name="paperformat_id" ref="report_pnt.paperformat_picking_label"/>-->  
<!--        &lt;!&ndash; para que aparezca en el menú Imprimir &ndash;&gt;-->  
<!--        <field name="binding_model_id" ref="stock.model_stock_picking"/>-->  
<!--        <field name="binding_type">report</field>-->  
<!--        &lt;!&ndash; pasar el contexto de si es etiqueta de entrada o salida &ndash;&gt;-->  
<!--    </record>-->  
  
<!--    &lt;!&ndash; 3) Acción de informe vinculada al picking &ndash;&gt;-->  
<!--    <record id="action_report_pnt_picking_label_out" model="ir.actions.report">-->  
<!--        <field name="name">Etiqueta de Salida</field>-->  
<!--        <field name="model">stock.picking</field>-->  
<!--        <field name="report_type">qweb-pdf</field>-->  
<!--        &lt;!&ndash; tu template QWeb principal &ndash;&gt;-->  
<!--        <field name="report_name">report_pnt.report_pnt_delivery_document_out</field>-->  
<!--        <field name="report_file">report_pnt.report_pnt_delivery_document_out</field>-->  
<!--        &lt;!&ndash; usa el paperformat que definimos arriba &ndash;&gt;-->  
<!--        <field name="paperformat_id" ref="report_pnt.paperformat_picking_label"/>-->  
<!--        &lt;!&ndash; para que aparezca en el menú Imprimir &ndash;&gt;-->  
<!--        <field name="binding_model_id" ref="stock.model_stock_picking"/>-->  
<!--        <field name="binding_type">report</field>-->  
<!--        &lt;!&ndash; pasar el contexto de si es etiqueta de entrada o salida &ndash;&gt;-->  
<!--    </record>-->  
  
    <!-- Acción de servidor para Imprimir Etiqueta de Entrada -->    <record id="action_server_pnt_picking_label_in" model="ir.actions.server">  
        <field name="name">Imprimir Etiqueta de Entrada</field>  
        <field name="model_id" ref="stock.model_stock_picking"/>  
        <field name="state">code</field>  
        <field name="code">action = env['ir.actions.report']._get_report_from_name('report_pnt.report_pnt_delivery_document_in').with_context(is_entry_label=True).report_action(record)</field>  
        <field name="binding_model_id" ref="stock.model_stock_picking"/>  
        <field name="binding_type">report</field>  
    </record>  
    <!-- Acción de servidor para Imprimir Etiqueta de Salida -->  
    <record id="action_server_pnt_picking_label_out" model="ir.actions.server">  
        <field name="name">Imprimir Etiqueta de Salida</field>  
        <field name="model_id" ref="stock.model_stock_picking"/>  
        <field name="state">code</field>  
        <field name="code">action = env['ir.actions.report']._get_report_from_name('report_pnt.report_pnt_delivery_document_out').with_context(is_entry_label=False).report_action(record)</field>  
        <field name="binding_model_id" ref="stock.model_stock_picking"/>  
        <field name="binding_type">report</field>  
    </record>
```