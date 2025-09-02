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

## receiveTrackingEvent

```json
{
  "metaData": {
    "senderID": "SwabCloth_ERP",
    "receiverClient": "SwabCloth",
    "receiverRole": "SUPPLIER",
    "senderRole": "SUPPLIER",
    "sendDate": {
      "dateInTimezone": "2020-10-10 17:04:20",
      "timezone": "Europe/Berlin"
    },
    "messageReferenceNumber": "ERP_2851408",
    "updateMode": "STANDARD",
    "idRefScheme": "SUPPLIER"
  },
  "head": {
    "identCode": "Shipped",
    "actualDate": {
      "dateInTimezone": "2020-10-10 17:04:20",
      "timezone": "Europe/Berlin"
    },
    "actualLocation": {
      "city": "Ludwigsburg",
      "countryISOCode": "DE",
      "postcodeStreet": "71634",
      "timezone": "Europe/Berlin",
      "globLocationNo": "SW_CLOTH_1"
    },
    "actualSender": {
      "globalLocationNumber": "SW_CLOTH",
      "name": "Swabian Clothes"
    }
  },
  "references": [
    {
      "trackingObjectType": "CONS",
      "referenceFields": [
        {
          "referenceField": "CONS_NO",
          "referenceNumber": "ERP_2851406_1"
        }
      ]
    }
  ]
}
```

## Result

## Order Status

![1083](https://files.readme.io/047450d-shipped_order.PNG "shipped_order.PNG")

## Shipment Status

![1113](https://files.readme.io/201614a-shipped_shipment.PNG "shipped_shipment.PNG")

## Track & Trace App

Shipments can also be viewed in the mobile friendly *Track & Trace* Webapp, which is reachable by adding */track-and-trace* to the end of the engine url.

![525](https://files.readme.io/e3fe187-track_and_trace_iphone.PNG "track_and_trace_iphone.PNG")

## Explanations

## references

`trackingObjectType`: Here we enter `CONS` for consignment, because we want to update the shipment.\
`referenceFields.referenceField`: We want to send the event to the shipment with the provided number.
