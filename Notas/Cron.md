> [[Back]]

Tags: 
Status: 
Related: 

___
# Cron
`client/custom_pnt/data/ir_cron.xml`
`aidimme`
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<odoo noupdate="1">
    <record id="pnt_check_certifications" model="ir.cron">
        <field name="name">[PNT] Check certificates</field>
        <field name="user_id">1</field>
        <field name="interval_number">1</field>
        <field name="interval_type">days</field>
        <field name="numbercall">-1</field>
        <field eval="False" name="doall"/>
        <field ref="custom_pnt.model_pnt_partner_certificate" name="model_id"/>
        <field name="state">code</field>
        <field name="code">model.cron_check_certificate()</field>
        <field name="active" eval="False" />
    </record>
</odoo>
```