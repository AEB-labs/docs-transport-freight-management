---
title: Retrieving tracking events for specific shipments
deprecated: false
hidden: true
metadata:
  robots: index
---
If you want to retrieve tracking events for specific shipments on demand, you can use the `getShipmentsEvents` method.

This method returns the complete tracking information currently available in Carrier Event Service (CES) for the provided shipment references. In contrast to event synchronization via `getEvents`, this call does not work with time ranges or `syncId`, but with explicitly provided shipment references.

### Request

You must provide the technical client context as well as at least one shipment reference.

The request contains:

* `clientSystemId`
* `clientIdentCode`
* `userName`
* `shipmentReferences` – list of shipments to retrieve
* Optional language and text flags:
  * `resultLanguageIsoCodes`
  * `isStandardEventTextIncluded`
  * `isOriginalDescriptionIncluded`

Each entry in `shipmentReferences` identifies a shipment, for example by:

* `shipmentNumber`
* `transactionId`
* `clientSystemId`
* `organizationUnitClientSystem`

<br />

<br />
