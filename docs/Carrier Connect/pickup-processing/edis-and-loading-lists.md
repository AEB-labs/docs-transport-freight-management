---
title: EDIs and loading lists
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
## Pickup processing

A previously generated pickup can be further processed using processPickup.

With the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processpickup" target="_blank">processPickup</a> call, it is possible to complete a partially processed collection including document printing and EDI dispatch in Carrier Connect. The corresponding parameters must be entered in the processParms.\
For referencing the pickup either the transaction ID, reference number 1, or the pickup number can be used as shown in the example below. 

```xml
<pickupReference>
   <transactionId></transactionId>
   <referenceNumber1></referenceNumber1>
   <pickupNumber>1004031</pickupNumber>
</pickupReference>
```

Parameters in which the processing and response can be handled are 'doManifest' which can be considered as a flag for completing the pickup and the 'documentOutputMode' in which existing loading lists can be triggered to be printed or returned in the response.

```xml
<processParms>
               <doManifest>true</doManifest>
               <documentOutputMode>
                  <mode>RETURN</mode>
               </documentOutputMode>
               <workstationId>MHD</workstationId>
            </processParms>
```
