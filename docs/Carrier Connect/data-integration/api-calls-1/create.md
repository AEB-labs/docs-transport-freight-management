---
title: Create
excerpt: >-
  Learn how to use the Carrier Connect API calls to programmatically CREATE new
  shipments or pickups.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    For more in depth information about specific sections of the API have a look
    at:
  pages:
    - type: basic
      slug: referencing-data
      title: 🔗 Referencing data
    - type: basic
      slug: additional-values-reference-fields
      title: 📑 Transmitting references & additional information
---
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

# createShipment: Create a new shipping order

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/createshipment" target="_blank">createShipment</a> call enables you to generate a new <Glossary>shipping order</Glossary> using the data provided in the shipment request. 

> 📘 Be aware, that if the shipment already exists, an error will be returned.

Furthermore, you can choose to apply various operations to the shipment, such as label preparation and output. It is even possible to complete the entire processing, including the assignment of a pickup.

<CreateShipmentGenericCarrierDomestic />

<br />

## Completing the shipment

<CompletingTheShipment />

# createPickup: Create a new pickup

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/createpickup" target="_blank">createPickup</a> call allows you to generate a new <Glossary>pickup</Glossary> for the shipments specified in your request. 

<Callout icon="💡" theme="default">
  ### Certain conditions result in error

  Please note, that certain conditions may result in an error, for example, when the shipments cannot be combined into a single pickup due to different carriers being involved.
</Callout>

Additionally, you have the option to manifest the new pickup. This process involves sending the necessary EDI to the carrier and subsequently closing the pickup. If specified in the request, manifest documents will be printed.

```json
{
  "clientSystemId": "YOUR_SYSTEM_ID",
  "clientIdentCode": "CCO_TEMPL",
  "userName": "WSM",
  "resultLanguageIsoCodes": [
    "en"
  ],
  "creationParms": {
    "creationMode": "ONLY_VALID_SHIPMENTS"
  },
  "pickup": {
    "transactionId": "2000006190",
    "referenceNumber1": "2000006190",
    "carrierIdentCode": "GENERICCARRIER",
    "shippingDate": "20230727",
    "shippingPt": {
       "companyNumber": "V1",
       "initFromCompanyMasterFileData": "true"
    },
    "shipments": [
      {
        "referenceNumber1": "1001"
      },
      {
        "referenceNumber1": "1002"
      },
    ]
  },
  "processParms": {
    "doManifest": false,
    "documentOutputMode": {
      "mode": "RETURN"
    },
    "workstationId": "PDF"
  }
}
```
```xml
<clientSystemId>YOUR_SYSTEM_ID</clientSystemId>
<clientIdentCode>CCO_TEMPL</clientIdentCode>
<userName>WSM</userName>
<resultLanguageIsoCodes>en</resultLanguageIsoCodes>
<creationParms>
  <creationMode>ONLY_VALID_SHIPMENTS</creationMode>
</creationParms>
<pickup>
  <transactionId>2000006190</transactionId>
  <referenceNumber1>2000006190</referenceNumber1>
  <carrierIdentCode>GENERICCARRIER</carrierIdentCode>
  <shippingDate>20230727</shippingDate>
  <shippingPt>
    <companyNumber>V1</companyNumber>
    <initFromCompanyMasterFileData>true</initFromCompanyMasterFileData>
  </shippingPt>
  <shipments>
    <shipment>
      <referenceNumber1>1001</referenceNumber1>
    </shipment>
    <shipment>
      <referenceNumber1>1002</referenceNumber1>
    </shipment>
  </shipments>
</pickup>
<processParms>
  <doManifest>false</doManifest>
  <documentOutputMode>
    <mode>RETURN</mode>
  </documentOutputMode>
  <workstationId>PDF</workstationId>
</processParms>
```
