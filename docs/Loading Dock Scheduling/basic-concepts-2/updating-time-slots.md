---
title: Updating Time Slots
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
## updateTimeSlotStatus

Sets the time slot of the loading order with the `OrderReferenceNumber` `Order_2851407` to status `BEGIN`.

```json
{
  "requestData": {
    "clientIdentCode": "JIL_DEMO"
  },
  "loadingOrderReference": {
    "referenceField": [
      {
        "referenceFieldName": "ORDERREFERENCENUMBER",
        "referenceFieldValue": "Order_2851407"
      }
    ]
  },
  "statusDateName": "BEGIN",
  "statusDateValue": "2020-11-11 14:06"
}
```
