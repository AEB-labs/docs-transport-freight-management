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
Synchronizing the Loading Orders from the Loading Dock Scheduling, can be done by using the `synchronizeLoadingOrders` call.

Doing so returns all the Loading Orders that have been created or changed since the provided `syncId`.\
The call also returns a syncId which can then be used in subsequent calls, for the first call use the syncId `0`.

```json
{
  "requestData": {
    "clientIdentCode": "SwabCloth"
  },
  "syncId": 1337
}
```
