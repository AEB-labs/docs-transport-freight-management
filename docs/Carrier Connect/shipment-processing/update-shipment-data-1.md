---
title: Updating shipment data
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
      slug: create-pickup
      title: Creating a pickup
---
When processing shipments, you have the possibility to update individual data on the shipment level within <a href="../../reference#processshipment" target="_blank">"processShipment"</a> request.

The data that can be changed is given in the overview. First of all, there is the section of totals within the shipment like number of packages, weights of the shipment, or total number of pallet places. Furthermore, there is the data of the shipment like shipping date or values concerning insurance and goods.
[block:code]
{
  "codes": [
    {
      "code": "            <shipmentTotals>\n               <numberOfPackagesExpected>?</numberOfPackagesExpected>\n               <grossWeightExpected>\n                  <value>?</value>\n                  <unit>?</unit>\n               </grossWeightExpected>\n               <loadingMeters>?</loadingMeters>\n               <palletPlaces>?</palletPlaces>\n            </shipmentTotals>\n            <shipmentUpdateData>\n               <shippingDate>?</shippingDate>\n               <codValue>\n                  <value>?</value>\n                  <currencyIso>?</currencyIso>\n               </codValue>\n               <insuranceValue>\n                  <value>?</value>\n                  <currencyIso>?</currencyIso>\n               </insuranceValue>\n               <goodsValue>\n                  <value>?</value>\n                  <currencyIso>?</currencyIso>\n               </goodsValue>\n               <customsValue>\n                  <value>?</value>\n                  <currencyIso>?</currencyIso>\n               </customsValue>\n               <customsRegistrationNumber>?</customsRegistrationNumber>\n               <remark>?</remark>\n            </shipmentUpdateData>\n",
      "language": "xml"
    }
  ]
}
[/block]
Another possibility is to update existing packages and move them to another shipment (this function is in the beta stage and may be deleted in further releases).

To archive the "move package" functionality, the operation mode in the process parameters has to be set to 'MOVE_PACKAGE'.
Accordingly, the section for target shipment reference has to be filled with the reference of the new shipment for moving the package to that shipment.
Prerequisite for moving a package is that the source and target shipments are not completed. Additionally, when a package is prepared for printing, the destination address, the service, and the account for both shipments have to be identical. Otherwise, an error will occur.
[block:code]
{
  "codes": [
    {
      "code": "<processParms>\n   <processMode>\n      <mode>EXTENDED</mode>\n   </processMode>\n   <documentPrepareMode>\n      <mode>PACKAGEONLY</mode>\n   </documentPrepareMode>\n   <workstationId>SDA</workstationId>\n      <documentOutputMode>\n      <mode>RETURN</mode>\n   </documentOutputMode>\n   <operationMode>\n      <mode>MOVE_PACKAGE</mode>\n   </operationMode>\n</processParms>\n<targetShipmentReference>\n   <transactionId></transactionId>\n   <referenceNumber1></referenceNumber1>\n   <shipmentNumber>SHIPMENT_NUMBER_TEST2</shipmentNumber>\n</targetShipmentReference>",
      "language": "xml"
    }
  ]
}
[/block]