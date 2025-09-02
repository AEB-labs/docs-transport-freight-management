---
title: Synchronizing Data
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
Synchronizing the Shipments from M&A, can be done by using the `syncConsignments` call.

Doing so returns all the Shipments that have been created or changed since the provided `syncId`.
The call also returns a syncId which can then be used in subsequent calls, for the first call use the syncId `0`.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"clientSystemId\": \"SwabCloth_ERP\",\n  \"clientIdentCode\": \"SwabCloth\",\n  \"userName\": \"GregorySmith\",\n  \"resultLanguageIsoCodes\": [\n    \"EN\"\n  ],\n  \"syncId\": \"1337\",\n  \"dataExtent\": [\n    \"INCLUDE_CONSIGNMENT_ITEMS\"\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]