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
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

# How to handle hazardous goods shipments

For general information about how hazardous goods are handled by Carrier Connect go to:

* <Anchor label="Understanding and enabling hazardous goods handling with Carrier Connect" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-en-US/t-801708043-667083787-en-US">Understanding and enabling hazardous goods handling with Carrier Connect</Anchor> [<Anchor label="German version" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-667083787-de-DE">German version</Anchor>]
* <Anchor label="Marking hazardous goods packages and creating new hazardous goods items in Carrier Connect" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-en-US/t-801708043-673169163-en-US">Marking hazardous goods packages and creating new hazardous goods items in Carrier Connect</Anchor> [<Anchor label="German version" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-673169163-de-DE">German version</Anchor>]

Hazardous goods handling has to be enabled in the carrier configuration for the specific client.

Hazardous goods shipment items can only be added on the shipment item level so far.
For EDIs, the carriers need to receive the data about hazardous goods on the package level.

Therefore in Carrier Connect, shipment items which include hazardous goods items have to packed in packages. Only then the package knows which hazardous goods are included and the correct data according to the EDI specification is sent to the carrier.

The example below shows a package with the reference number 'SHIPMENT_PACK_TEST1' which contains an item 'SHIPMENT_TEST1'. This item contains a hazardous goods item with UN number '1845' (=dry ice).
When the EDI generation is creating the data, the hazardous goods item with UN number '1845' and its data would appear under the related package with the reference number 'SHIPMENT_PACK_TEST1' segment which would satisfy the carrier's requirements.

Package level:

```json
{
  "shipment": {
    "packages": [
      {
        "hazardousGoodsData": {
          "hazardousGoodsType": "NORMAL"
        }
      }
    ]
  }
}
```
```xml
<shipment>
    <packages>
        <hazardousGoodsData>
            <hazardousGoodsType>NORMAL</hazardousGoodsType>
        </hazardousGoodsData>
    </packages>
</shipment>
```

As shown in the example, each package containing hazardous goods need a hazardous goods type indication as well.

Available hazardous goods types are:

* NONE (no hazardous goods)
* NORMAL (hazardous goods)
* EQ (excepted quantities)
* LQ (limited quantities)
* SPECIAL_SUBSTANCE (special substance)
* ORMD (other regulated materials for domestic transport only) - Since 2021 this code is not used anymore
* US_SMALL_QUANTITY (small quantity regulated materials) - only relevant for US

Item level:

```json
{
  "shipment": {
    "items": [
      {
        "hazardousGoodsItems": [
          {
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
            "specialSubstanceType": "DRY_ICE",
            "isOuterPackage": true,
            "isEnvironmentallyHazardous": true
          }
        ]
      }
    ]
  }
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

<br />
