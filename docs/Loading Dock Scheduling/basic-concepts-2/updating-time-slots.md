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
[block:api-header]
{
  "title": "updateTimeSlotStatus"
}
[/block]
Sets the time slot of the loading order with the `OrderReferenceNumber` `Order_2851407` to status `BEGIN`.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"requestData\": {\n    \"clientIdentCode\": \"JIL_DEMO\"\n  },\n  \"loadingOrderReference\": {\n    \"referenceField\": [\n      {\n        \"referenceFieldName\": \"ORDERREFERENCENUMBER\",\n        \"referenceFieldValue\": \"Order_2851407\"\n      }\n    ]\n  },\n  \"statusDateName\": \"BEGIN\",\n  \"statusDateValue\": \"2020-11-11 14:06\"\n}",
      "language": "json"
    }
  ]
}
[/block]