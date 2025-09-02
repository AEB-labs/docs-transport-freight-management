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
[block:api-header]
{
  "title": "Pickup processing"
}
[/block]
A previously generated pickup can be further processed using processPickup.

With the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processpickup" target="_blank">processPickup</a> call, it is possible to complete a partially processed collection including document printing and EDI dispatch in Carrier Connect. The corresponding parameters must be entered in the processParms.
For referencing the pickup either the transaction ID, reference number 1, or the pickup number can be used as shown in the example below. 
[block:code]
{
  "codes": [
    {
      "code": "<pickupReference>\n   <transactionId></transactionId>\n   <referenceNumber1></referenceNumber1>\n   <pickupNumber>1004031</pickupNumber>\n</pickupReference>\n",
      "language": "xml"
    }
  ]
}
[/block]
Parameters in which the processing and response can be handled are 'doManifest' which can be considered as a flag for completing the pickup and the 'documentOutputMode' in which existing loading lists can be triggered to be printed or returned in the response.
[block:code]
{
  "codes": [
    {
      "code": "            <processParms>\n               <doManifest>true</doManifest>\n               <documentOutputMode>\n                  <mode>RETURN</mode>\n               </documentOutputMode>\n               <workstationId>MHD</workstationId>\n            </processParms>",
      "language": "xml"
    }
  ]
}
[/block]