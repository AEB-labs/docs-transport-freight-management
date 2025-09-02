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

```xml
<shipmentTotals>
               <numberOfPackagesExpected>?</numberOfPackagesExpected>
               <grossWeightExpected>
                  <value>?</value>
                  <unit>?</unit>
               </grossWeightExpected>
               <loadingMeters>?</loadingMeters>
               <palletPlaces>?</palletPlaces>
            </shipmentTotals>
            <shipmentUpdateData>
               <shippingDate>?</shippingDate>
               <codValue>
                  <value>?</value>
                  <currencyIso>?</currencyIso>
               </codValue>
               <insuranceValue>
                  <value>?</value>
                  <currencyIso>?</currencyIso>
               </insuranceValue>
               <goodsValue>
                  <value>?</value>
                  <currencyIso>?</currencyIso>
               </goodsValue>
               <customsValue>
                  <value>?</value>
                  <currencyIso>?</currencyIso>
               </customsValue>
               <customsRegistrationNumber>?</customsRegistrationNumber>
               <remark>?</remark>
            </shipmentUpdateData>
```

Another possibility is to update existing packages and move them to another shipment (this function is in the beta stage and may be deleted in further releases).

To archive the "move package" functionality, the operation mode in the process parameters has to be set to 'MOVE\_PACKAGE'.\
Accordingly, the section for target shipment reference has to be filled with the reference of the new shipment for moving the package to that shipment.\
Prerequisite for moving a package is that the source and target shipments are not completed. Additionally, when a package is prepared for printing, the destination address, the service, and the account for both shipments have to be identical. Otherwise, an error will occur.

```xml
<processParms>
   <processMode>
      <mode>EXTENDED</mode>
   </processMode>
   <documentPrepareMode>
      <mode>PACKAGEONLY</mode>
   </documentPrepareMode>
   <workstationId>SDA</workstationId>
      <documentOutputMode>
      <mode>RETURN</mode>
   </documentOutputMode>
   <operationMode>
      <mode>MOVE_PACKAGE</mode>
   </operationMode>
</processParms>
<targetShipmentReference>
   <transactionId></transactionId>
   <referenceNumber1></referenceNumber1>
   <shipmentNumber>SHIPMENT_NUMBER_TEST2</shipmentNumber>
</targetShipmentReference>
```
