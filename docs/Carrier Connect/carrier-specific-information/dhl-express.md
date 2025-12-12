---
title: DHL Express (Germany)
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Export data

For more information see our [Help Center Article](https://service.aeb.com/hc/de/articles/4413696305297-DHL-Express-Zollpflichtige-Daten-f%C3%BCr-Drittlandversand-%C3%BCbermitteln-und-ggf-DHL-Paperless-Trade-PLT-in-Carrier-Connect-nutzen).

```json
"additionalValues": {
      "fields": [
        {
          "name": "DHLEXPINTEXPRSN",
          "type": "string",
          "value": "PERMANENT"
        },
        {
          "name": "DHLEXPINTINVDATE",
          "type": "dateTime",
          "value": "2024-01-18T00:00:00"
        },
        {
          "name": "DHLEXPINTINVAMOU",
          "type": "decimal",
          "value": "100.00"
        },
        {
          "name": "DHLEXPINTINVCURR",
          "type": "string",
          "value": "EUR"
        }
      ]
    },
 "referencesTexts": [
      {
        "type": "INVOICE_NUMBER",
        "value": "INV1234567"
      }
    ],
```
```xml
<additionalValues>
  <fields>
    <field>
      <name>DHLEXPINTEXPRSN</name>
      <type>string</type>
      <value>PERMANENT</value>
    </field>
    <field>
      <name>DHLEXPINTINVDATE</name>
      <type>dateTime</type>
      <value>2024-01-18T00:00:00</value>
    </field>
    <field>
      <name>DHLEXPINTINVAMOU</name>
      <type>decimal</type>
      <value>100.00</value>
    </field>
    <field>
      <name>DHLEXPINTINVCURR</name>
      <type>string</type>
      <value>EUR</value>
    </field>
  </fields>
</additionalValues>
<referencesTexts>
  <referenceText>
    <type>INVOICE_NUMBER</type>
    <value>INV1234567</value>
  </referenceText>
</referencesTexts>
```

# MOA