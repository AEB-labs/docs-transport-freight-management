---
title: Packing Items
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
    
    color: red;
  }
</style>
`}</HTMLBlock>

# Packed items

Some carriers or some shipping scenarios (e.g. dangerous goods) require that items are not just listed within the shipment, but they must be assigned to packages.

## How to pack items

The following example shows how to pack items using the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/createshipment" target="_blank">createShipment</a> (but you can also use the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processshipment" target="_blank">processShipment</a>) call.

```json
{
  "packages": [
    {
      "packageTypeIdentCode": "BOX",
      "packageNumber": "1",
      "packageTransactionId": "PACKAGE_TEST_1",
      "referenceNumber1": "PACKAGE_TEST_1",
      "grossWeight": {
        "value": "25",
        "unit": "kg"
      },
      "containedItems": [
        {
          "itemTransactionId": "ITEM_TEST_1",
          "referenceNumber1": "ITEM_TEST_1",
          "quantityValue": "10"
        }
      ]
    }
  ]
}
```
```xml
<packages>
   <packageTypeIdentCode>BOX</packageTypeIdentCode>
   <packageNumber>1</packageNumber>
   <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
   <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
   <grossWeight>
      <value>25</value>
      <unit>kg</unit>
   </grossWeight>
   <containedItems>
      <itemTransactionId>ITEM_TEST_1</itemTransactionId>
      <referenceNumber1>ITEM_TEST_1</referenceNumber1>
      <quantityValue>10</quantityValue>
   </containedItems>
</packages>
```

If you're using XML, you can repeat *n* times:

```xml
<packages>
  ...
  <containedItems>Item 1</containedItems>  
  <containedItems>Item 2</containedItems>  
  ...  
  <containedItems>Item n</containedItems>
</packages>
```

<br />

> ❗️
>
> You can't pack items into packages with the `processPackage` call!
