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
Synchronizing the Shipments from M\&A, can be done by using the `syncConsignments` call.

Doing so returns all the Shipments that have been created or changed since the provided `syncId`.\
The call also returns a syncId which can then be used in subsequent calls, for the first call use the syncId `0`.

```json
{
  "clientSystemId": "SwabCloth_ERP",
  "clientIdentCode": "SwabCloth",
  "userName": "GregorySmith",
  "resultLanguageIsoCodes": [
    "EN"
  ],
  "syncId": "1337",
  "dataExtent": [
    "INCLUDE_CONSIGNMENT_ITEMS"
  ]
}
```
