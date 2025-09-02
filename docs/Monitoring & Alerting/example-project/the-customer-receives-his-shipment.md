---
title: The customer receives his shipment
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
  "title": "receiveTrackingEvent"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"metaData\": {\n    \"senderID\": \"SwabCloth_ERP\",\n    \"receiverClient\": \"SwabCloth\",\n    \"receiverRole\": \"SUPPLIER\",\n    \"senderRole\": \"SUPPLIER\",\n    \"sendDate\": {\n      \"dateInTimezone\": \"2020-10-12 13:04:20\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"messageReferenceNumber\": \"ERP_2851408\",\n    \"updateMode\": \"STANDARD\",\n    \"idRefScheme\": \"SUPPLIER\"\n  },\n  \"head\": {\n    \"identCode\": \"Shipped\",\n    \"actualDate\": {\n      \"dateInTimezone\": \"2020-10-12 13:04:20\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"actualLocation\": {\n      \"city\": \"Ludwigsburg\",\n      \"countryISOCode\": \"DE\",\n      \"postcodeStreet\": \"71634\",\n      \"timezone\": \"Europe/Berlin\",\n      \"globLocationNo\": \"SW_CLOTH_1\"\n    },\n    \"actualSender\": {\n      \"globalLocationNumber\": \"SW_CLOTH\",\n      \"name\": \"Swabian Clothes\"\n    }\n  },\n  \"references\": [\n    {\n      \"trackingObjectType\": \"CONS\",\n      \"referenceFields\": [\n        {\n          \"referenceField\": \"CONS_NO\",\n          \"referenceNumber\": \"ERP_2851406_1\"\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/477f648-shipment_finished.PNG",
        "shipment_finished.PNG",
        751,
        143,
        "#ceebd7"
      ]
    }
  ]
}
[/block]