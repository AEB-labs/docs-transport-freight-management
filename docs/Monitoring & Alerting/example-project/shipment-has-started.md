---
title: Shipment has started
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
The carrier picks up the shipment that was created in the previous. Now we want that our order as well as our shipment reflect the new status.

To do so, we send an event to the shipment, the event then propagates to the corresponding order event, because of our master data configuration. See [Master Data](doc:master-data).
[block:api-header]
{
  "title": "receiveTrackingEvent"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"metaData\": {\n    \"senderID\": \"SwabCloth_ERP\",\n    \"receiverClient\": \"SwabCloth\",\n    \"receiverRole\": \"SUPPLIER\",\n    \"senderRole\": \"SUPPLIER\",\n    \"sendDate\": {\n      \"dateInTimezone\": \"2020-10-10 17:04:20\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"messageReferenceNumber\": \"ERP_2851408\",\n    \"updateMode\": \"STANDARD\",\n    \"idRefScheme\": \"SUPPLIER\"\n  },\n  \"head\": {\n    \"identCode\": \"Shipped\",\n    \"actualDate\": {\n      \"dateInTimezone\": \"2020-10-10 17:04:20\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"actualLocation\": {\n      \"city\": \"Ludwigsburg\",\n      \"countryISOCode\": \"DE\",\n      \"postcodeStreet\": \"71634\",\n      \"timezone\": \"Europe/Berlin\",\n      \"globLocationNo\": \"SW_CLOTH_1\"\n    },\n    \"actualSender\": {\n      \"globalLocationNumber\": \"SW_CLOTH\",\n      \"name\": \"Swabian Clothes\"\n    }\n  },\n  \"references\": [\n    {\n      \"trackingObjectType\": \"CONS\",\n      \"referenceFields\": [\n        {\n          \"referenceField\": \"CONS_NO\",\n          \"referenceNumber\": \"ERP_2851406_1\"\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Result"
}
[/block]
## Order Status
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/047450d-shipped_order.PNG",
        "shipped_order.PNG",
        1083,
        511,
        "#e9eff0"
      ]
    }
  ]
}
[/block]
## Shipment Status
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/201614a-shipped_shipment.PNG",
        "shipped_shipment.PNG",
        1113,
        418,
        "#e5edee"
      ]
    }
  ]
}
[/block]
## Track & Trace App

Shipments can also be viewed in the mobile friendly *Track & Trace* Webapp, which is reachable by adding */track-and-trace* to the end of the engine url.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e3fe187-track_and_trace_iphone.PNG",
        "track_and_trace_iphone.PNG",
        525,
        892,
        "#b4b2bb"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Explanations"
}
[/block]
## references

`trackingObjectType`: Here we enter `CONS` for consignment, because we want to update the shipment.
`referenceFields.referenceField`: We want to send the event to the shipment with the provided number.