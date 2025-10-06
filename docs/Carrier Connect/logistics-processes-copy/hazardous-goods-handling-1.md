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

Hazardous goods handling has to be enabled in the carrier configuration:

<Image border={false} src="https://files.readme.io/3c5357f6983bbcd0a697953378b201b8d28eacd4b8e233debf33f042bf89f03e-image.png" />

Hazardous goods shipment items can only be added on the shipment item level so far. For EDIs, the carriers need to receive the data about hazardous goods on the package level. **Therefore, in Carrier Connect, shipment items which include hazardous goods items have to packed in packages.** Only then the package knows which hazardous goods are included and the correct data according to the EDI specification is sent to the carrier. For more information about how to pack items see [Packing Items](doc:cma-shipping-scenarios).

## Package level

On package level each package containing hazardous goods need a hazardous goods type indication:

```json
{
  "shipment": {
    "packages": [
      {
        "packageNumber": "1",
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
        <packageNumber>1</packageNumber>
        <hazardousGoodsData>
            <hazardousGoodsType>NORMAL</hazardousGoodsType>
        </hazardousGoodsData>
    </packages>
</shipment>
```

Available hazardous goods types are:

* NONE (no hazardous goods)
* NORMAL (hazardous goods)
* EQ (excepted quantities)
* LQ (limited quantities)
* SPECIAL_SUBSTANCE (special substance)
* ORMD (other regulated materials for domestic transport only) - Since 2021 this code is not used anymore
* US_SMALL_QUANTITY (small quantity regulated materials) - only relevant for US

## Item level

On item level there are 

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
            "tunnelCode": "1A1",
            "hazardWeight": {
              "value": 20,
              "unit": "kg"
            },
            "numberOfPackages": 1,
            "packageTypeIdentCode": "CARTON",
            "specialSubstanceType": "DRY_ICE"
          }
        ]
      }
    ]
  }
}
```
```xml
<shipment>
    <items>
        <hazardousGoodsItems>
            <unNumber>1845</unNumber>
            <hazardRegulation>IATA</hazardRegulation>
            <technicalName>Dry Ice</technicalName>
            <hazardClass>2</hazardClass>
            <tunnelCode>1A1</tunnelCode>
            <hazardWeight>
                <value>20</value>
                <unit>kg</unit>
            </hazardWeight>
            <numberOfPackages>1</numberOfPackages>
            <packageTypeIdentCode>CARTON</packageTypeIdentCode>
            <specialSubstanceType>DRY_ICE</specialSubstanceType>
        </hazardousGoodsItems>
    </items>
</shipment>
```

<br />
