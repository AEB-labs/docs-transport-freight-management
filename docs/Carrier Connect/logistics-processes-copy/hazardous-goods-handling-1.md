---
title: Hazardous goods handling
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## How to handle hazardous goods shipments

Hazardous goods handling has to be enabled in the carrier configuration for the specific client.

Hazardous goods shipment items can only be added on the shipment item level so far.\
For EDIs, the carriers need to receive the data about hazardous goods on the package level. 

Therefore in Carrier Connect, shipment items which include hazardous goods items have to packed in packages. Only then the package knows which hazardous goods are included and the correct data according to the EDI specification is sent to the carrier.

The example below shows a package with the reference number 'SHIPMENT\_PACK\_TEST1' which contains an item 'SHIPMENT\_TEST1'. This item contains a hazardous goods item with UN number '1845' (=dry ice).\
When the EDI generation is creating the data, the hazardous goods item with UN number '1845' and its data would appear under the related package with the reference number 'SHIPMENT\_PACK\_TEST1' segment which would satisfy the carrier's requirements.

```json
{
    "packages": [{
            "packageTypeIdentCode": "KRT",
            "packageNumber": 1,
            "packageTransactionId": 1,
            "referenceNumber1": "SHIPMENT_PACK_TEST1",
            "referenceNumber2": "SHIPMENT_PACK_TEST1",
            "grossWeight": {
                "value": 25,
                "unit": "kg"
            },
            "containedItems": {
                "itemTransactionId": "SHIPMENT_TEST",
                "referenceNumber1": "SHIPMENT_TEST1",
                "quantityValue": 10
            },
            "hazardousGoodsData": {
                "hazardousGoodsType": "NORMAL"
            }
        }
    ],
    "items": [{
            "itemNumber": 1,
            "itemTransactionId": "SHIPMENT_TEST",
            "referenceNumber1": "SHIPMENT_TEST1",
            "description": "Schrauben",
            "countryOfOriginsISOCode": "DE",
            "certificateOfOrigins": "DE",
            "quantity": {
                "value": 10,
                "unit": "St"
            },
            "customsValue": {
                "value": 100,
                "currencyIso": "EUR"
            },
            "goodsValue": {
                "value": 100,
                "currencyIso": "EUR"
            },
            "hazardousGoodsItems": [{
                "unNumber": 1845,
                "hazardRegulation": "IATA",
                "technicalName": "Dry Ice",
                "hazardClass": 2,
                "classificationCode": "3T",
                "hazardCharacteristics": "ätzend",
                "tunnelCode": "1A1",
                "hazardInducer": "H2O",
                "hazardWeight": {
                    "value": 20,
                    "unit": "kg"
                },
                "numberOfPackages": 1,
                "hazardLabel": "LABEL",
                "hazardPoints": 100,
                "flashPoint": 115,
                "specialSubstanceType": "DRY_ICE",
                "isOuterPackage": true,
                "isEnvironmentallyHazardous": true
            }]
        }
    ]
}
```
```xml
<packages>
   <packageTypeIdentCode>KRT</packageTypeIdentCode>
   <packageNumber>1</packageNumber>
   <packageTransactionId>1</packageTransactionId>
   <referenceNumber1>SHIPMENT_PACK_TEST1</referenceNumber1>
   <referenceNumber2>SHIPMENT_PACK_TEST1</referenceNumber2>
   <grossWeight>
      <value>25</value>
      <unit>kg</unit>
   </grossWeight>
   <containedItems>
      <itemTransactionId>SHIPMENT_TEST</itemTransactionId>
      <referenceNumber1>SHIPMENT_TEST1</referenceNumber1>
      <quantityValue>10</quantityValue>
   </containedItems>
   <hazardousGoodsData>
      <hazardousGoodsType>NORMAL</hazardousGoodsType>
   </hazardousGoodsData>
</packages>

<items>
   <itemNumber>1</itemNumber>
	 <itemTransactionId>SHIPMENT_TEST</itemTransactionId>
	 <referenceNumber1>SHIPMENT_TEST1</referenceNumber1>
	 <description>Schrauben</description>
	 <countryOfOriginsISOCode>DE</countryOfOriginsISOCode>
	 <certificateOfOrigins>DE</certificateOfOrigins>
	 <quantity>
	    <value>10</value>
	    <unit>St</unit>
	 </quantity>
	 <customsValue>
	    <value>100</value>
	    <currencyIso>EUR</currencyIso>
	 </customsValue>
	 <goodsValue>
	    <value>100</value>
	    <currencyIso>EUR</currencyIso>
	 </goodsValue>
   <hazardousGoodsItems>
      <unNumber>1845</unNumber>
      <hazardRegulation>IATA</hazardRegulation>
      <technicalName>Dry Ice</technicalName>
      <hazardClass>2</hazardClass>
      <subriskClass1></subriskClass1>
      <subriskClass2></subriskClass2>
      <classificationCode>3T</classificationCode>
      <hazardCharacteristics>ätzend</hazardCharacteristics>
      <tunnelCode>1A1</tunnelCode>
      <hazardInducer>H2O</hazardInducer>
      <packagingGroup></packagingGroup>
      <packageTypeIdentCode></packageTypeIdentCode>
      <hazardWeight>
         <value>20</value>
         <unit>kg</unit>
      </hazardWeight>
      <numberOfPackages>1</numberOfPackages>
      <hazardLabel>LABEL</hazardLabel>
      <hazardPoints>100</hazardPoints>
      <flashPoint>115</flashPoint>
      <specialSubstanceType>DRY_ICE</specialSubstanceType>
      <isOuterPackage>true</isOuterPackage>
      <isEnvironmentallyHazardous>true</isEnvironmentallyHazardous>
   </hazardousGoodsItems>
</items>
```

As shown in the example, the package needs a hazardous goods type indication as well.

Available hazardous goods types are:\
'NONE' (=No hazardous goods) -DEFAULT-\
'NORMAL' (=Normal hazardous goods)\
'LQ' (=Limited quantity)\
'EQ' (=Excepted quantity)\
'SPECIAL\_SUBSTANCE' (=special substance)\
'US\_SMALL\_QUANTITY' (=Small Quantity (US relevant))
