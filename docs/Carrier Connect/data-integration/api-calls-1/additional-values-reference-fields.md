---
title: Transmitting references & additional information
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

# Extended information: References and texts

<Callout icon="💡" theme="default">
  ### German: Referenztexte
</Callout>

![](https://files.readme.io/e0c9f61-image.png)

Reference texts can be used to transmit standardized types of information to Carrier Connect. These fields are often used as additional shipment data. However, **not every text will be transmitted to the carrier. This depends on the carrier and their systems.**

```json

"shipment": {
  "referencesTexts": [
    {
      "type": "PO_NUMBER",
      "value": "order123456789"
    }
  ],
  ...
}
  
```
```xml
<shipment>
  <referencesTexts>
      <type>PO_NUMBER</type>
      <value>order123456789</value>
  </referencesTexts>
  ...
</shipment>
```

To use these references and texts there are two fields to be filled:

* `type`: Name of the reference field. All valid types are listed in the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/createshipment" target="_blank">API Reference</a> of Carrier Connect.
* `value`: Value of the reference field.

# Extra fields

<Callout icon="💡" theme="default">
  ### German: Zusatzfelder
</Callout>

![](https://files.readme.io/7d8bf47-image.png)

There are two usecases for extra fields: 

1. A carrier can require specific information for each shipment, that are not typically needed by other carriers. 
2. The fields can be customer-specific and help with the process control. 

To use an extra field in Carrier Connect, there are three fields to be considered: 

* `name`: The name of the additional value field (available in the carrier configuration). 
* `type`: The type of format that is used for the value. 
* `value`: The actual value of the field. 

```json
"shipment": {
  "additionalValues": {
    "fields": [
      {
        "name": "ACCNO",
        "type": "string",
        "value": "123456"
      }
    ]
  }
}
```
```xml
<shipment>
  <additionalValues>
      <fields>
          <name>ACCNO</name>
          <type>string</type>
          <value>123456</value>
      </fields>
  </additionalValues>
  ...
</shipment>
```

Depending on the type of field there are different formats. All valid types are listed in the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/createshipment" target="_blank">API Reference</a> of Carrier Connect.

<Zusatzleistungen />

<br />

<Hinweistexte />
