---
title: Deleting a package
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
[block:api-header]
{
  "title": "For deleting a package"
}
[/block]
If a specific package in a shipment has to be deleted, the deletePackage method is used to perform the task.
Use <a href="https://transport-freight-management.docs.developers.aeb.com/reference/deletepackage" target="_blank">deletePackage</a> with e.g. the *shipment number* of the shipment and the *referenceNumber1* as reference to the package to delete the package from a shipment.

The configuration of the client in Carrier Connect defines whether it is allowed to delete a package from a shipment. Options for deleting packages are 'Always allowed', 'Not, if assigned to a package and documents exist' and 'Not allowed'.
[block:code]
{
  "codes": [
    {
      "code": "<packageReference>\n   <shipmentReference>\n      <transactionId>SHIPMENT_TEST2</transactionId>\n      <referenceNumber1>SHIPMENT_TEST1</referenceNumber1>\n      <shipmentNumber>SHIPMENT_TEST1</shipmentNumber>\n   </shipmentReference>\n   <packageTransactionId>SHIPMENT_TEST</packageTransactionId>\n   <referenceNumber1>SHIPMENT_TEST3</referenceNumber1>\n</packageReference>\n",
      "language": "xml"
    }
  ]
}
[/block]