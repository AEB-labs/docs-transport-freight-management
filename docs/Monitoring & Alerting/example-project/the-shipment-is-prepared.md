---
title: The shipment is prepared
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
In the next step a worker has packed the ordered items on a pallet and they are ready for transport, while the DHL (the carrier) already received the job and we have received a tracking number and label for our goods.

Once this is done, we send a message to create the <Glossary>Shipment</Glossary> object with the shipment items in the Monitoring & Alerting platform.

## receiveConsignmentWithTransport

In order to create the shipment with the two shipment items and the transport we call the `receiveConsignmentWithTransport` method with the following data.

```json
{
  "metaData": {
    "senderID": "SwabCloth_ERP",
    "receiverClient": "SwabCloth",
    "receiverRole": "SUPPLIER",
    "senderRole": "SUPPLIER",
    "sendDate": {
      "dateInTimezone": "2020-10-10 15:33:34",
      "timezone": "Europe/Berlin"
    },
    "messageReferenceNumber": "ERP_2851407",
    "messageType": "SHIPMENT",
    "updateMode": "STANDARD",
    "idRefScheme": "SUPPLIER"
  },
  "head": {
    "consignmentNumber": "ERP_2851406_1",
    "termsOfDelivery": {
      "incotermCode": "FCA",
      "incotermDestination": "Stuttgart",
      "termsOfDeliveryCode": "FCA"
    },
    "shipperReference": "ERP_2851406_1",
    "consignmentType": "Shipment - Textiles",
    "buyer": {
      "globalLocationNumber": "1000",
      "name": "FunClothes",
      "street": "Haupstraße 405",
      "postcodeStreet": "10115",
      "city": "Berlin",
      "countryISOCode": "DE",
      "timezone": "Europe/Berlin",
      "emailAddress": "mainoffice@FunClothes.de"
    },
    "consignee": {
      "globalLocationNumber": "1000_1",
      "name": "FunClothes - Stuttgart location",
      "street": "Schlossallee 404",
      "postcodeStreet": "70173",
      "city": "Stuttgart",
      "countryISOCode": "DE",
      "timezone": "Europe/Berlin",
      "emailAddress": "stuttgart@FunClothes.de"
    },
    "supplier": {
      "globalLocationNumber": "SW_CLOTH",
      "name": "Swabian Clothes"
    },
    "shippingPoint": {
      "globalLocationNumber": "SW_CLOTH_1",
      "name": "SW Ludwigsburg shipment center",
      "street": "Industriestraße 123",
      "postcodeStreet": "71634",
      "city": "Ludwigsburg",
      "countryISOCode": "DE",
      "timezone": "Europe/Berlin"
    },
    "forwarderPickup": {
      "globalLocationNumber": "DHL",
      "name": "DHL"
    },
    "forwarderDeliv": {
      "globalLocationNumber": "DHL",
      "name": "DHL"
    },
    "carrierPickup": {
      "globalLocationNumber": "DHL",
      "name": "DHL"
    },
    "carrierDeliv": {
      "globalLocationNumber": "DHL",
      "name": "DHL"
    },
    "expectedShippingDate": {
      "dateInTimezone": "2020-10-10 17:00:00",
      "timezone": "Europe/Berlin"
    },
    "palletSlots": 1,
    "goodsDescription": "Textiles",
    "latestDeliveryDate": {
      "dateInTimezone": "2020-10-17 11:11:34",
      "timezone": "Europe/Berlin"
    }
  },
  "items": [
    {
      "itemNumber": "1",
      "orderItemNumberSupplier": "ERP_2851406_1",
      "orderNumberSupplier": "ERP_2851406",
      "buyer": {
        "globalLocationNumber": "1000",
        "name": "FunClothes",
        "street": "Haupstraße 405",
        "postcodeStreet": "10115",
        "city": "Berlin",
        "countryISOCode": "DE",
        "timezone": "Europe/Berlin",
        "emailAddress": "mainoffice@FunClothes.de"
      },
      "supplier": {
        "globalLocationNumber": "SW_CLOTH",
        "name": "Swabian Clothes"
      },
      "consignee": {
        "globalLocationNumber": "1000_1",
        "name": "FunClothes - Stuttgart location",
        "street": "Schlossallee 404",
        "postcodeStreet": "70173",
        "city": "Stuttgart",
        "countryISOCode": "DE",
        "timezone": "Europe/Berlin",
        "emailAddress": "stuttgart@FunClothes.de"
      },
      "shippingPoint": {
        "globalLocationNumber": "SW_CLOTH_1",
        "name": "SW Ludwigsburg shipment center",
        "street": "Industriestraße 123",
        "postcodeStreet": "71634",
        "city": "Ludwigsburg",
        "countryISOCode": "DE"
      },
      "material": {
        "identCode": "shirt_plain_white",
        "productGroup1Supplier": "textiles",
        "productGroup2Supplier": "upper_body",
        "shortDescription": "Plain white T-Shirt.",
        "size": "L",
        "colour": "white"
      },
      "quantitySendBySupplier": {
        "value": 200,
        "quantityUnit": "pc"
      },
      "goodsValue": {
        "value": 800,
        "currencyISOCode": "EUR"
      }
    },
    {
      "itemNumber": "2",
      "orderItemNumberSupplier": "ERP_2851406_2",
      "orderNumberSupplier": "ERP_2851406",
      "buyer": {
        "globalLocationNumber": "1000",
        "name": "FunClothes",
        "street": "Haupstraße 405",
        "postcodeStreet": "10115",
        "city": "Berlin",
        "countryISOCode": "DE",
        "timezone": "Europe/Berlin",
        "emailAddress": "mainoffice@FunClothes.de"
      },
      "supplier": {
        "globalLocationNumber": "SW_CLOTH",
        "name": "Swabian Clothes"
      },
      "consignee": {
        "globalLocationNumber": "1000_1",
        "name": "FunClothes - Stuttgart location",
        "street": "Schlossallee 404",
        "postcodeStreet": "70173",
        "city": "Stuttgart",
        "countryISOCode": "DE",
        "timezone": "Europe/Berlin",
        "emailAddress": "stuttgart@FunClothes.de"
      },
      "shippingPoint": {
        "globalLocationNumber": "SW_CLOTH_1",
        "name": "SW Ludwigsburg shipment center",
        "street": "Industriestraße 123",
        "postcodeStreet": "71634",
        "city": "Ludwigsburg",
        "countryISOCode": "DE"
      },
      "material": {
        "identCode": "jeans_blue",
        "productGroup1Supplier": "textiles",
        "productGroup2Supplier": "lower_body",
        "shortDescription": "Plain blue jeans",
        "size": "L",
        "colour": "blue"
      },
      "quantitySendBySupplier": {
        "value": 100,
        "quantityUnit": "pc"
      },
      "goodsValue": {
        "value": 680,
        "currencyISOCode": "EUR"
      }
    }
  ],
  "transports": [
    {
      "metaData": {
        "senderID": "SwabCloth_ERP",
        "receiverClient": "SwabCloth",
        "receiverRole": "SUPPLIER",
        "senderRole": "SUPPLIER",
        "sendDate": {
          "dateInTimezone": "2020-10-10 15:33:34",
          "timezone": "Europe/Berlin"
        },
        "messageReferenceNumber": "ERP_2851407_Transport_1",
        "updateMode": "STANDARD",
        "idRefScheme": "SUPPLIER"
      },
      "head": {
        "consignmentNumber": "ERP_2851406_1",
        "masterWayBillNumber": "123456789",
        "plannedDepartureDate": {
          "dateInTimezone": "2020-10-10 17:00:00",
          "timezone": "Europe/Berlin"
        },
        "startLoc": {
          "city": "Ludwigsburg",
          "countryISOCode": "DE",
          "postcodeStreet": "71634",
          "timezone": "Europe/Berlin",
          "globLocationNo": "SW_CLOTH_1"
        },
        "endLoc": {
          "city": "Stuttgart",
          "countryISOCode": "DE",
          "postcodeStreet": "70173",
          "timezone": "Europe/Berlin",
          "globLocationNo": "1000_1"
        },
        "supplier": {
          "globalLocationNumber": "SW_CLOTH",
          "name": "Swabian Clothes"
        },
        "globalTransactionNumber": "ERP_2851406_1_Transport_1"
      }
    }
  ]
}
```

## Result

The call creates a shipment, two shipment items and a transport.

## Search

![1258](https://files.readme.io/3d7c1d2-receiveConsignmentWithTransport_search.PNG "receiveConsignmentWithTransport_search.PNG")

## Shipment Navigator

![1467](https://files.readme.io/954bdf0-receiveConsignmentWithTransport_navigator.PNG "receiveConsignmentWithTransport_navigator.PNG")

## Explanations

## items

The data for the shipment items is filled here.

It is essential that the `orderNumberSupplier`, `supplier.globalLocationNumber` and the `orderItemNumberSupplier`, like they are filled in the corresponding order item and order, because these fields are used to calculate the reference that connects the shipment item to the order item in the `SUPPLIER` scheme.

More information about id and references calculation can be found at [Object IDs & References](doc:referencing-data-1).

# transport

`masterWayBillNumber` This field is filled with tracking number received from DHL.
