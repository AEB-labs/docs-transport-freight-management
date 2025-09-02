---
title: Synchronizing shipments
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
A further possibility for requesting shipments from a calling system is given with <a href="https://carrierconnect.docs.developers.aeb.com/reference#syncshipments-1" target="_blank">syncShipments</a>.

The call is identical to "getShipments", with the difference that the returned shipping orders are the ones that have changed since the last syncShipments call.

For the request, a sync ID or a parameter named 'ageInDays' have to be filled in to get the corresponding shipments from Carrier Connect.

The following is an example for the syncShipments request:

```xml
<request>
   <clientSystemId>SOAPUI</clientSystemId>
   <clientIdentCode>ADMIN</clientIdentCode>
   <userName>ADMIN</userName>
   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>
   <syncId></syncId>
   <ageInDays>2</ageInDays>
   <includeDocuments>false</includeDocuments>
</request>
```
