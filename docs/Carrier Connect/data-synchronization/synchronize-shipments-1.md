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
[block:code]
{
  "codes": [
    {
      "code": "<request>\n   <clientSystemId>SOAPUI</clientSystemId>\n   <clientIdentCode>ADMIN</clientIdentCode>\n   <userName>ADMIN</userName>\n   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>\n   <syncId></syncId>\n   <ageInDays>2</ageInDays>\n   <includeDocuments>false</includeDocuments>\n</request>",
      "language": "xml"
    }
  ]
}
[/block]