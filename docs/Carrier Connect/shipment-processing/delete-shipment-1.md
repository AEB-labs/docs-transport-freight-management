---
title: Deleting a shipment
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
## Canceling a shipment

If a shipment has to be canceled, <a href="https://transport-freight-management.docs.developers.aeb.com/reference/cancelshipment" target="_blank">cancelShipment</a> can be used. There is no deleteShipment because shipments cannot be canceled unlike packages or shipment items. The reference for an existing shipment can be e.g. a *shipment number* or the *transaction id*.

```xml
<shipmentReference>
   <transactionId></transactionId>
   <referenceNumber1>SHIPMENT_TEST2</referenceNumber1>
   <shipmentNumber>9009450</shipmentNumber>
</shipmentReference>
```
