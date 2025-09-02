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
A further possibility for requesting shipments from a calling system is given with <a href="https://transport-freight-management.docs.developers.aeb.com/reference/syncshipments" target="_blank">syncShipments</a>.

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
There is a limit of 100 shipments per syncShipment call. As long as the number of shipments in the answer equals 100, there are still more shipments to synchronize. This limit is built in so that a single call does not request an indefinite number of shipments and thus paralyze the system.

If the number returned equals 100, then further syncShipment calls could follow directly with the last syncId transmitted until less than 100 shipments are synced back.

- The value for the next syncShipment call is transferred in the response to the syncShipment call in the field syncId.
- Initially you can start the syncShipment call with syncId = 0 or 1.
- With syncID = -1 you can query VAs that do not have a completed status. Explanation needed: when do shipments have a completed status? (How does -1 change to the current syncID -> Batch)