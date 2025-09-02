---
title: Creating a pickup
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
In a common scenario, the carriers request an EDI file with all relevant shipments which were transported by the carrier at the end of a working day. This is important when it comes to freight costs or planning of logistical issues in the carrier's process, e.g. fast and correct forwarding in the hub of the carrier. Therefore, a request with createPickup has to be triggered.

The <a href="https://carrierconnect.docs.developers.aeb.com/reference#createpickup-1" target="_blank">createPickup</a> method can be used to create pickups for specific carriers in Carrier Connect. The data must be entered in the DTO DLCreatePickupRequestDTO.
Depending on the parameters set in the creationParms and processParms, there are different usage scenarios.

  * Complete handling of a pickup: creation of a pickup, assignment of the contained shipments, printing of the collection documents (loading lists), sending of the EDI (if necessary), completion.
  * Partial processing of a pickup: Only creation of a pickup and assignment of the shipments. Shipments can then be added or removed via the GUI. Attention: There is no interface functionality for this.

The *transaction id* or the *reference number 1* can be used as references for getting the correct pickup and *transaction id*, *reference number 1*, or *shipment number*.
[block:code]
{
  "codes": [
    {
      "code": "<transactionId></transactionId>\n<transactionLabel></transactionLabel>\n<referenceNumber1>1</referenceNumber1>\n<shipments>\n   <transactionId>SHIPMENT_TEST3</transactionId>\n   <referenceNumber1>SHIPMENT_TEST7</referenceNumber1>\n   <shipmentNumber>9009450</shipmentNumber>\n</shipments>\n",
      "language": "xml"
    }
  ]
}
[/block]