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
## Package by Package

One or several packages can be added quickly to an existing shipment via <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processshipment" target="_blank">processShipment</a> using e.g. the *shipment number* as reference.

The *transactionId* and/or the *referenceNumber1* can be used as alternative or additional references.\
**Note:** The *referenceNumber1* does not have to be unique. Consequently, the *transactionId* or the *shipmentNumber* should be used to reference a shipment to ensure that the correct shipment is addressed.\
These possible references are combined in the *shipmentReference* (DTO). Again, it is possible to use all of them or only one and leave the other outs:

```xml
<shipmentReference>
       <transactionId>?</transactionId>
       <referenceNumber1>?</referenceNumber1>
       <shipmentNumber>?</shipmentNumber>
</shipmentReference>
```

A package is described within the *<packages>* tag. It has its own references and attributes.

```xml
<packages>
         <packageTypeIdentCode>?</packageTypeIdentCode>
         <packageSpecificeContents>?</packageSpecificeContents>
         <packageNumber>?</packageNumber>
         <packageTransactionId>?</packageTransactionId>
         <referenceNumber1>?</referenceNumber1>
         <referenceNumber2>?</referenceNumber2>
         <grossWeight>
              <value>?</value>
              <unit>?</unit>
          </grossWeight>
          <dimensions>
              <length>?</length>
              <width>?</width>
              <height>?</height>
              <identCode>?</identCode>
          </dimensions>
          ...
</packages>
```

Additionally, it can include packed items or references on items. However, *qualified packing* is only required for <a href="https://transport-freight-management.docs.developers.aeb.com/docs/hazardous-goods-handling-1" target="_blank">hazardous good shipping</a>.

```xml
<packages>
  ...
      <alternativeVolume>
          <value>?</value>
          <unit>?</unit>
      </alternativeVolume>
      <codValue>
          <value>?</value>
          <currencyIso>?</currencyIso>
      </codValue>
      <additionalValues>
          <fields>
              <name>?</name>
              <type>?</type>
              <value>?</value>
          </fields>
      </additionalValues>
      <containedItems>
          <shipmentReference>
              <transactionId>?</transactionId>
              <referenceNumber1>?</referenceNumber1>
              <shipmentNumber>?</shipmentNumber>
          </shipmentReference>
          <itemTransactionId>?</itemTransactionId>
          <referenceNumber1>?</referenceNumber1>
          <quantityValue>?</quantityValue>
      </containedItems>
      <hazardousGoodsData>
          <hazardousGoodsType>?</hazardousGoodsType>
      </hazardousGoodsData>
  ...
</packages>
```