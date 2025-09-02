---
title: Managing Loading Orders
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
This page explains api methods regarding Loading Orders and offers a small sample message for each method.
[block:api-header]
{
  "title": "createLoadingOrder"
}
[/block]
Use this to create a Loading Order.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"requestData\": {\n    \"clientIdentCode\": \"SwabCloth\",\n    \"installationIdHost\": \"ERP_123\"\n  },\n  \"loadingOrder\": {\n    \"referenceNumber\": \"Order_2851407\",\n    \"loadingType\": \"LOADING\",\n    \"forwarderReference\": \"CoolForwarder\",\n    \"forwarder\": {\n      \"contact\": {\n        \"surname\": \"Peter\",\n        \"forename\": \"Hans\",\n        \"title\": \"MR\",\n        \"phoneNumber\": \"+49123456789\",\n        \"email\": \"HansPeter@CoolForwarder.io\",\n        \"language\": \"DE\"\n      },\n      \"name1\": \"Cool Forwarder SE\",\n      \"city\": \"Berlin\",\n      \"postcode\": \"10369\",\n      \"countryIsoCode\": \"DE\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"vehicleDriver\": {\n      \"surname\": \"Schmitt\",\n      \"forename\": \"Gerhard\",\n      \"title\": \"MR\",\n      \"phoneNumber\": \"+49987654321\",\n      \"email\": \"GerhardSchmitt@CoolForwarder.io\"\n    },\n    \"timeSlotRequirements\": {\n      \"loadingLocation\": \"STR\",\n      \"timeSlotLengthMinutes\": 90\n    },\n    \"transportType\": \"Container\"\n  },\n  \"notifyForwarder\":true\n}",
      "language": "json"
    }
  ]
}
[/block]
## Notifications
Setting `notifyForwarder: true`, will automatically send an E-mail with the Text as defined in the master data for *Notification type*: `Email: order information` to the mail set in the forwarder contact.
[block:api-header]
{
  "title": "updateLoadingOrder"
}
[/block]
Updates a Loading order, where the field `OrderReferenceNumber` is `Order_2851407` with a new `vehicleLicenseNumber`.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"clientSystemId\": \"ERP_123\",\n  \"clientIdentCode\": \"SwabCloth\",\n  \"userName\": \"GregorySmith\",\n  \"resultLanguageIsoCodes\": [\n    \"EN\"\n  ],\n  \"loadingOrderReference\": {\n    \"referenceField\": [\n      {\n        \"referenceFieldName\": \"ORDERREFERENCENUMBER\",\n        \"referenceFieldValue\": \"Order_2851407\"\n      }\n    ]\n  },\n  \"notifyForwarder\": false,\n  \"loadingOrder\": {\n    \"vehicleLicenseNumber\": \"B-CF-1337\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "getLoadingOrder"
}
[/block]
Retrieves the data for a Loading Order where the field `OrderReferenceNumber` is `Order_2851407`.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"requestData\": {\n    \"clientIdentCode\": \"SwabCloth\"\n  },\n  \"loadingOrderReference\": {\n    \"referenceField\": [\n      {\n        \"referenceFieldName\": \"ORDERREFERENCENUMBER\",\n        \"referenceFieldValue\": \"Order_2851407\"\n      }\n    ]\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]