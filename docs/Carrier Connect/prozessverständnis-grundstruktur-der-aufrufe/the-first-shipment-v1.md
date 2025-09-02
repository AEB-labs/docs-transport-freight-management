---
title: 🥇 The First Shipment (OLD)
excerpt: Prepared calls for copy/paste in your development environment
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: common-shipping-scenarios
      title: Common shipping scenarios
---
[block:html]
{
  "html": "<style>\n  span.cm-s-neo {\n    background-color: #f2f2f2;\n    color: red;\n  }\n</style>"
}
[/block]


To allow you to start quickly, here you will find a complete call to create a shipment and receive a typical response.

# Creating a shipment

You can use the example and copy/paste it into your favorite tool to test SOAP and/or REST API calls. Our test environment is prepared to work with the data in this example.  
Why don't you just give it a quick try?

Below is an example `createShipment` call for a domestic shipment. You can find it in your test client with the shipment number 1000001: 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/43bb33ed9aca1981bc4bb644592ae786377dba7cb19c1b3f3ebc8411ac772c81-image.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


![](https://files.readme.io/260eb23dc2b7a39bb75ea5d82b23c0a5fedb6dbc35d64d9cb647437b026685b3-image.png)

<br />

<CreateShipmentGenericCarrierDomestic />

And here another example. This time for a third country shipment. You can find it in your test client with the shipment number 1000000:

<CreateShipmentGenericCarrierExport />

<br />

# The API response

<CCOAPIResponse />

<br />

# Receiving an error

Below is an API response with an error. This will demonstrate the structure of an error response and will allow you to become familiar with the general behavior.  
You will receive this message once you remove `clientSystemId` from the above request.

```json
{
   "hasErrors":"true",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "messages":{
      "messageType":"ERROR",
      "messageIdentCode":"EMPTY_MANDATORY_FIELD",
      "messageTexts":{
         "languageISOCode":"en",
         "text":"Client system id not filled."
      },
      "indentationLevel":"0"
   }
}
```
```xml
<createShipmentResponse>
   <result>
      <hasErrors>true</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <messages>
         <messageType>ERROR</messageType>
         <messageIdentCode>EMPTY_MANDATORY_FIELD</messageIdentCode>
         <messageTexts>
            <languageISOCode>en</languageISOCode>
            <text>Client system id not filled.</text>
         </messageTexts>
         <indentationLevel>0</indentationLevel>
      </messages>
   </result>
</createShipmentResponse>
```