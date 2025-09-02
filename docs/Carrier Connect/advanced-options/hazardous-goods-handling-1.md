---
title: Hazardous goods handling
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
  "title": "How to handle hazardous goods shipments"
}
[/block]
Hazardous goods handling has to be enabled in the carrier configuration for the specific client.

Hazardous goods shipment items can only be added on the shipment item level so far.
For EDIs, the carriers need to receive the data about hazardous goods on the package level. 

Therefore in Carrier Connect, shipment items which include hazardous goods items have to packed in packages. Only then the package knows which hazardous goods are included and the correct data according to the EDI specification is sent to the carrier.

The example below shows a package with the reference number 'SHIPMENT_PACK_TEST1' which contains an item 'SHIPMENT_TEST1'. This item contains a hazardous goods item with UN number '1845' (=dry ice).
When the EDI generation is creating the data, the hazardous goods item with UN number '1845' and its data would appear under the related package with the reference number 'SHIPMENT_PACK_TEST1' segment which would satisfy the carrier's requirements.
[block:code]
{
  "codes": [
    {
      "code": "<packages>\n   <packageTypeIdentCode>KRT</packageTypeIdentCode>\n   <packageNumber>1</packageNumber>\n   <packageTransactionId>1</packageTransactionId>\n   <referenceNumber1>SHIPMENT_PACK_TEST1</referenceNumber1>\n   <referenceNumber2>SHIPMENT_PACK_TEST1</referenceNumber2>\n   <grossWeight>\n      <value>25</value>\n      <unit>kg</unit>\n   </grossWeight>\n   <containedItems>\n      <itemTransactionId>SHIPMENT_TEST</itemTransactionId>\n      <referenceNumber1>SHIPMENT_TEST1</referenceNumber1>\n      <quantityValue>10</quantityValue>\n   </containedItems>\n   <hazardousGoodsData>\n      <hazardousGoodsType>NORMAL</hazardousGoodsType>\n   </hazardousGoodsData>\n</packages>\n\n<items>\n   <itemNumber>1</itemNumber>\n\t <itemTransactionId>SHIPMENT_TEST</itemTransactionId>\n\t <referenceNumber1>SHIPMENT_TEST1</referenceNumber1>\n\t <description>Schrauben</description>\n\t <countryOfOriginsISOCode>DE</countryOfOriginsISOCode>\n\t <certificateOfOrigins>DE</certificateOfOrigins>\n\t <quantity>\n\t    <value>10</value>\n\t    <unit>St</unit>\n\t </quantity>\n\t <customsValue>\n\t    <value>100</value>\n\t    <currencyIso>EUR</currencyIso>\n\t </customsValue>\n\t <goodsValue>\n\t    <value>100</value>\n\t    <currencyIso>EUR</currencyIso>\n\t </goodsValue>\n   <hazardousGoodsItems>\n      <unNumber>1845</unNumber>\n      <hazardRegulation>IATA</hazardRegulation>\n      <technicalName>Dry Ice</technicalName>\n      <hazardClass>2</hazardClass>\n      <subriskClass1></subriskClass1>\n      <subriskClass2></subriskClass2>\n      <classificationCode>3T</classificationCode>\n      <hazardCharacteristics>ätzend</hazardCharacteristics>\n      <tunnelCode>1A1</tunnelCode>\n      <hazardInducer>H2O</hazardInducer>\n      <packagingGroup></packagingGroup>\n      <packageTypeIdentCode></packageTypeIdentCode>\n      <hazardWeight>\n         <value>20</value>\n         <unit>kg</unit>\n      </hazardWeight>\n      <numberOfPackages>1</numberOfPackages>\n      <hazardLabel>LABEL</hazardLabel>\n      <hazardPoints>100</hazardPoints>\n      <flashPoint>115</flashPoint>\n      <specialSubstanceType>DRY_ICE</specialSubstanceType>\n      <isOuterPackage>true</isOuterPackage>\n      <isEnvironmentallyHazardous>true</isEnvironmentallyHazardous>\n   </hazardousGoodsItems>\n</items>",
      "language": "xml"
    }
  ]
}
[/block]
As shown in the example, the package needs a hazardous goods type indication as well.

Available hazardous goods types are:
'NONE' (=No hazardous goods) -DEFAULT-
'NORMAL' (=Normal hazardous goods)
'LQ' (=Limited quantity)
'EQ' (=Excepted quantity)