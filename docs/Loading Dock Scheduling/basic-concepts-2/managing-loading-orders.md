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

## createLoadingOrder

Use this to create a Loading Order.

```json
{
  "requestData": {
    "clientIdentCode": "SwabCloth",
    "installationIdHost": "ERP_123"
  },
  "loadingOrder": {
    "referenceNumber": "Order_2851407",
    "loadingType": "LOADING",
    "forwarderReference": "CoolForwarder",
    "forwarder": {
      "contact": {
        "surname": "Peter",
        "forename": "Hans",
        "title": "MR",
        "phoneNumber": "+49123456789",
        "email": "HansPeter@CoolForwarder.io",
        "language": "DE"
      },
      "name1": "Cool Forwarder SE",
      "city": "Berlin",
      "postcode": "10369",
      "countryIsoCode": "DE",
      "timezone": "Europe/Berlin"
    },
    "vehicleDriver": {
      "surname": "Schmitt",
      "forename": "Gerhard",
      "title": "MR",
      "phoneNumber": "+49987654321",
      "email": "GerhardSchmitt@CoolForwarder.io"
    },
    "timeSlotRequirements": {
      "loadingLocation": "STR",
      "timeSlotLengthMinutes": 90
    },
    "transportType": "Container"
  },
  "notifyForwarder":true
}
```

## Notifications

Setting `notifyForwarder: true`, will automatically send an E-mail with the Text as defined in the master data for *Notification type*: `Email: order information` to the mail set in the forwarder contact.

## updateLoadingOrder

Updates a Loading order, where the field `OrderReferenceNumber` is `Order_2851407` with a new `vehicleLicenseNumber`.

```json
{
  "clientSystemId": "ERP_123",
  "clientIdentCode": "SwabCloth",
  "userName": "GregorySmith",
  "resultLanguageIsoCodes": [
    "EN"
  ],
  "loadingOrderReference": {
    "referenceField": [
      {
        "referenceFieldName": "ORDERREFERENCENUMBER",
        "referenceFieldValue": "Order_2851407"
      }
    ]
  },
  "notifyForwarder": false,
  "loadingOrder": {
    "vehicleLicenseNumber": "B-CF-1337"
  }
}
```

## getLoadingOrder

Retrieves the data for a Loading Order where the field `OrderReferenceNumber` is `Order_2851407`.

```json
{
  "requestData": {
    "clientIdentCode": "SwabCloth"
  },
  "loadingOrderReference": {
    "referenceField": [
      {
        "referenceFieldName": "ORDERREFERENCENUMBER",
        "referenceFieldValue": "Order_2851407"
      }
    ]
  }
}
```
