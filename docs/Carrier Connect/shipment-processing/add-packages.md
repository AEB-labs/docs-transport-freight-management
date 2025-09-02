---
title: Adding packages
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
  pages:
    - type: basic
      slug: add-items-1
      title: Adding items
---
[block:api-header]
{
  "title": "Package by Package"
}
[/block]
One or several packages can be added quickly to an exisiting shipment via <a href="https://carrierconnect.docs.developers.aeb.com/reference#processshipment-1" target="_blank">processShipment</a> using e.g. the *shipment number* as reference.

The *transactionId* and/or the *referenceNumber1* can be used as alternative or additional references.
**Note:** The *referenceNumber1* does not have to be unique. Consequently, the *transactionId* or the *shipmentNumber* should be used to reference a shipment to ensure that the correct shipment is addressed.
These possible refrences are combined in the *shipmentReference* (DTO). Again, it is possible to use all of them or only one and leave the other outs:
[block:code]
{
  "codes": [
    {
      "code": " <shipmentReference>\n       <transactionId>?</transactionId>\n       <referenceNumber1>?</referenceNumber1>\n       <shipmentNumber>?</shipmentNumber>\n </shipmentReference>\n",
      "language": "xml"
    }
  ]
}
[/block]
A package is described within the *<packages>* tag. It has its own references and attributes.
[block:code]
{
  "codes": [
    {
      "code": "<packages>\n         <packageTypeIdentCode>?</packageTypeIdentCode>\n         <packageSpecificeContents>?</packageSpecificeContents>\n         <packageNumber>?</packageNumber>\n         <packageTransactionId>?</packageTransactionId>\n         <referenceNumber1>?</referenceNumber1>\n         <referenceNumber2>?</referenceNumber2>\n         <grossWeight>\n              <value>?</value>\n              <unit>?</unit>\n          </grossWeight>\n          <dimensions>\n              <length>?</length>\n              <width>?</width>\n              <height>?</height>\n              <identCode>?</identCode>\n           </dimensions>\n              ...\n</packages>",
      "language": "xml"
    }
  ]
}
[/block]
Additonally, it can include packed items or references on items. However, *qualified packing* is only required for <a href="https://carrierconnect.docs.developers.aeb.com/docs/hazardous-goods-handling-1" target="_blank">hazardous good shipping</a>.
[block:code]
{
  "codes": [
    {
      "code": "<packages>\n  ...\n\t\t\t<alternativeVolume>\n                  <value>?</value>\n                  <unit>?</unit>\n               </alternativeVolume>\n               <codValue>\n                  <value>?</value>\n                  <currencyIso>?</currencyIso>\n               </codValue>\n               <additionalValues>\n                  <fields>\n                     <name>?</name>\n                     <type>?</type>\n                     <value>?</value>\n                  </fields>\n               </additionalValues>\n               <containedItems>\n                  <shipmentReference>\n                     <transactionId>?</transactionId>\n                     <referenceNumber1>?</referenceNumber1>\n                     <shipmentNumber>?</shipmentNumber>\n                  </shipmentReference>\n                  <itemTransactionId>?</itemTransactionId>\n                  <referenceNumber1>?</referenceNumber1>\n                  <quantityValue>?</quantityValue>\n               </containedItems>\n               <hazardousGoodsData>\n                  <hazardousGoodsType>?</hazardousGoodsType>\n               </hazardousGoodsData>\n \t\t ...\n  </packages>",
      "language": "xml"
    }
  ]
}
[/block]