> [[Modificaciones comunes Informes XML]]

Tags: 
Status: 
Related: 

___

# dato en informe segun si es str o int

<td name="day_amount"  
    class="text-end">  
    <t t-if="isinstance(day_amount, str)">  
        <t t-esc="day_amount"/>  
    </t>  
    <t t-else="">  
        <t t-esc="day_amount" t-options="{'widget': 'float', 'precision': 2}"/>  
    </t>  
</td>
```xml
<td name="day_amount"  
    class="text-end">  
    <t t-if="isinstance(day_amount, str)">  
        <t t-esc="day_amount"/>  
    </t>  
    <t t-else="">  
        <t t-esc="day_amount" t-options="{'widget': 'float', 'precision': 2}"/>  
    </t>  
</td>
```