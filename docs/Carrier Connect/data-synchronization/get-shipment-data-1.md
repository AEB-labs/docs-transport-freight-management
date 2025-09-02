---
title: Getting shipment data
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
Two specific API calls are available for requesting data.

The first one is <a href="https://transport-freight-management.docs.developers.aeb.com/reference/getshipments" target="_blank">getShipments</a> which queries the data of one or more shipping orders that are specified in the request using reference numbers.\
Optionally, the request can be triggered in such a way that the response includes the generated labels. This is for a scenario where the calling system handles label printing on its own.\
Another optional parameter is to return shipments which are in the 'Canceled' status.

The possibilities for referencing one specific shipment are (like in other cases/requests) either the transaction ID, reference number 1, or the shipment number.

A complete request looks like below:

```xml
<request>
   <clientSystemId>SOAPUI</clientSystemId>
   <clientIdentCode>ADMIN</clientIdentCode>
   <userName>ADMIN</userName>
   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>
   <shipmentReferences>
      <transactionId>SHIPMENT_TEST_HAZ</transactionId>
      <referenceNumber1>SHIPMENT_TEST</referenceNumber1>
      <shipmentNumber></shipmentNumber>
   </shipmentReferences>
   <includeDocuments>true</includeDocuments>
   <withCanceledShipments>false</withCanceledShipments>
</request>
```
