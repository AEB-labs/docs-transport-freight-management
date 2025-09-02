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
## receiveTrackingEvent

```json
{
  "metaData": {
    "senderID": "SwabCloth_ERP",
    "receiverClient": "SwabCloth",
    "receiverRole": "SUPPLIER",
    "senderRole": "SUPPLIER",
    "sendDate": {
      "dateInTimezone": "2020-10-12 13:04:20",
      "timezone": "Europe/Berlin"
    },
    "messageReferenceNumber": "ERP_2851408",
    "updateMode": "STANDARD",
    "idRefScheme": "SUPPLIER"
  },
  "head": {
    "identCode": "Shipped",
    "actualDate": {
      "dateInTimezone": "2020-10-12 13:04:20",
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

![751](https://files.readme.io/477f648-shipment_finished.PNG "shipment_finished.PNG")
