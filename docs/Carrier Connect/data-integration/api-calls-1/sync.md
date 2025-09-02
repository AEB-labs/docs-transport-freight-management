---
title: Sync and Get calls
excerpt: Learn how to synchronize shipping data programmatically using our sync calls.
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

# syncShipments

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/syncshipments" target="_blank">syncShipments</a> call returns all shipping orders that have changed since the last `syncShipments` call. To utilize this feature, you must provide either a <Glossary>syncID</Glossary> or fill in the <Glossary>ageInDays</Glossary> parameter.

## Using `syncId`

The `syncId` field is used to manage delta transmissions in synchronization calls. It helps in fetching only the data that has changed since the last synchronization.

Here’s how it works:

1. **Initial Call**: When making the first synchronization call, the `syncId` should be empty or set to a specific initial value (e.g., 0). This call will return all relevant data up to the current point.
2. **Subsequent Calls**: The response from the initial call will include a new syncId. For subsequent synchronization calls, this syncId should be used. This ensures that only the data that has changed since the last call is returned.

<Image align="center" src="https://files.readme.io/be72956-Sync.png" />

### Handling Large Data Sets

There is a limit of 100 shipments per `syncShipment` call. As long as the number of shipments in the answer equals 100, there are still more shipments to synchronize. 

This limit is built in so that a single call does not request an indefinite number of shipments and thus paralyze the system.

If the number returned equals 100, then further `syncShipment` calls could follow directly with the last `syncId` transmitted until less than 100 shipments are synced back.

* The value for the next syncShipment call is transferred in the response to the syncShipment call in the field syncId.
* Initially you can start the syncShipment call with syncId = 0 or 1.
* With syncID = -1 you can query <Glossary>shipping order</Glossary>s  that do not have a completed status.

## Using `ageInDays`

Below is an optimized example of a `syncShipments` request using the `ageInDays` parameter. This request will return all shipping orders with a shipping date within the last two days, excluding documents from the response:

```json
{
  "clientSystemId": "ERP",
  "clientIdentCode": "ADMIN",
  "userName": "ADMIN",
  "resultLanguageIsoCodes": "DE",
  "syncId": "",
  "ageInDays": 2,
  "includeDocuments": false
}
```
```xml
<clientSystemId>ERP</clientSystemId>
<clientIdentCode>ADMIN</clientIdentCode>
<userName>ADMIN</userName>
<resultLanguageIsoCodes>DE</resultLanguageIsoCodes>
<syncId></syncId>
<ageInDays>2</ageInDays>
<includeDocuments>false</includeDocuments>
```

# syncPickups

The sync for pickups works similar to the  `syncShipment` call via [syncPickups](https://transport-freight-management.docs.developers.aeb.com/reference/syncpickups)

# getShipments

To use <a href="https://transport-freight-management.docs.developers.aeb.com/reference/getshipments" target="_blank">getShipments</a>, you need to provide either reference numbers or a filter.

## Reference numbers

The getShipments call can be used to request the data of one or more <Glossary>shipping order</Glossary>s using reference numbers. To reference a specific shipment, you can use either the transaction ID, reference number 1, or the shipment number.

A complete request using reference numbers looks like below:

```json
{
  "request": {
    "clientSystemId": "ERP",
    "clientIdentCode": "ADMIN",
    "userName": "ADMIN",
    "resultLanguageIsoCodes": "DE",
    "shipmentReferences": {
      "transactionId": "123abc",
      "referenceNumber1": "",
      "shipmentNumber": ""
    },
    "includeDocuments": true,
    "withCanceledShipments": false
  }
}
```
```xml
<request>
   <clientSystemId>ERP</clientSystemId>
   <clientIdentCode>ADMIN</clientIdentCode>
   <userName>ADMIN</userName>
   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>
   <shipmentReferences>
      <transactionId>123abc</transactionId>
      <referenceNumber1></referenceNumber1>
      <shipmentNumber></shipmentNumber>
   </shipmentReferences>
   <includeDocuments>true</includeDocuments>
   <withCanceledShipments>false</withCanceledShipments>
</request>
```

## Filter

Instead of using reference numbers you can use filters. For more details about what filter options are available go to the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/getshipments" target="_blank">getShipments</a> documentation.

A request using the *shippingDateFrom* and *shippingDateTo* of the filter section:

```xml
<request>
   <clientSystemId>ERP</clientSystemId>
   <clientIdentCode>ADMIN</clientIdentCode>
   <userName>ADMIN</userName>
   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>
   <filter>
       <shippingDateFrom>20230315</shippingDateFrom>
       <shippingDateTo>20230322</shippingDateTo>
  </filter>
</request>
```
```json
{
  "request": {
    "clientSystemId": "ERP",
    "clientIdentCode": "ADMIN",
    "userName": "ADMIN",
    "resultLanguageIsoCodes": "DE",
    "filter": {
      "shippingDateFrom": 20230315,
      "shippingDateTo": 20230322
    }
  }
}
```

## More options

You also have the option to include generated labels in the response (by setting the "includeDocuments" parameter to "true"). This is useful if your system handles label printing on its own.

Additionally, you can choose to retrieve shipments that are in the "Canceled" status by setting the "withCanceledShipments" parameter to "true".
