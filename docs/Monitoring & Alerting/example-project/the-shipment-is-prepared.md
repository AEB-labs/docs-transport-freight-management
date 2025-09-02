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

Once this is done, we send a message to create the <<glossary:Shipment>> object with the shipment items in the Monitoring & Alerting platform.
[block:api-header]
{
  "title": "receiveConsignmentWithTransport"
}
[/block]
In order to create the shipment with the two shipment items and the transport we call the `receiveConsignmentWithTransport` method with the following data.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"metaData\": {\n    \"senderID\": \"SwabCloth_ERP\",\n    \"receiverClient\": \"SwabCloth\",\n    \"receiverRole\": \"SUPPLIER\",\n    \"senderRole\": \"SUPPLIER\",\n    \"sendDate\": {\n      \"dateInTimezone\": \"2020-10-10 15:33:34\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"messageReferenceNumber\": \"ERP_2851407\",\n    \"messageType\": \"SHIPMENT\",\n    \"updateMode\": \"STANDARD\",\n    \"idRefScheme\": \"SUPPLIER\"\n  },\n  \"head\": {\n    \"consignmentNumber\": \"ERP_2851406_1\",\n    \"termsOfDelivery\": {\n      \"incotermCode\": \"FCA\",\n      \"incotermDestination\": \"Stuttgart\",\n      \"termsOfDeliveryCode\": \"FCA\"\n    },\n    \"shipperReference\": \"ERP_2851406_1\",\n    \"consignmentType\": \"Shipment - Textiles\",\n    \"buyer\": {\n      \"globalLocationNumber\": \"1000\",\n      \"name\": \"FunClothes\",\n      \"street\": \"Haupstraße 405\",\n      \"postcodeStreet\": \"10115\",\n      \"city\": \"Berlin\",\n      \"countryISOCode\": \"DE\",\n      \"timezone\": \"Europe/Berlin\",\n      \"emailAddress\": \"mainoffice@FunClothes.de\"\n    },\n    \"consignee\": {\n      \"globalLocationNumber\": \"1000_1\",\n      \"name\": \"FunClothes - Stuttgart location\",\n      \"street\": \"Schlossallee 404\",\n      \"postcodeStreet\": \"70173\",\n      \"city\": \"Stuttgart\",\n      \"countryISOCode\": \"DE\",\n      \"timezone\": \"Europe/Berlin\",\n      \"emailAddress\": \"stuttgart@FunClothes.de\"\n    },\n    \"supplier\": {\n      \"globalLocationNumber\": \"SW_CLOTH\",\n      \"name\": \"Swabian Clothes\"\n    },\n    \"shippingPoint\": {\n      \"globalLocationNumber\": \"SW_CLOTH_1\",\n      \"name\": \"SW Ludwigsburg shipment center\",\n      \"street\": \"Industriestraße 123\",\n      \"postcodeStreet\": \"71634\",\n      \"city\": \"Ludwigsburg\",\n      \"countryISOCode\": \"DE\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"forwarderPickup\": {\n      \"globalLocationNumber\": \"DHL\",\n      \"name\": \"DHL\"\n    },\n    \"forwarderDeliv\": {\n      \"globalLocationNumber\": \"DHL\",\n      \"name\": \"DHL\"\n    },\n    \"carrierPickup\": {\n      \"globalLocationNumber\": \"DHL\",\n      \"name\": \"DHL\"\n    },\n    \"carrierDeliv\": {\n      \"globalLocationNumber\": \"DHL\",\n      \"name\": \"DHL\"\n    },\n    \"expectedShippingDate\": {\n      \"dateInTimezone\": \"2020-10-10 17:00:00\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"palletSlots\": 1,\n    \"goodsDescription\": \"Textiles\",\n    \"latestDeliveryDate\": {\n      \"dateInTimezone\": \"2020-10-17 11:11:34\",\n      \"timezone\": \"Europe/Berlin\"\n    }\n  },\n  \"items\": [\n    {\n      \"itemNumber\": \"1\",\n      \"orderItemNumberSupplier\": \"ERP_2851406_1\",\n      \"orderNumberSupplier\": \"ERP_2851406\",\n      \"buyer\": {\n        \"globalLocationNumber\": \"1000\",\n        \"name\": \"FunClothes\",\n        \"street\": \"Haupstraße 405\",\n        \"postcodeStreet\": \"10115\",\n        \"city\": \"Berlin\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"mainoffice@FunClothes.de\"\n      },\n      \"supplier\": {\n        \"globalLocationNumber\": \"SW_CLOTH\",\n        \"name\": \"Swabian Clothes\"\n      },\n      \"consignee\": {\n        \"globalLocationNumber\": \"1000_1\",\n        \"name\": \"FunClothes - Stuttgart location\",\n        \"street\": \"Schlossallee 404\",\n        \"postcodeStreet\": \"70173\",\n        \"city\": \"Stuttgart\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"stuttgart@FunClothes.de\"\n      },\n      \"shippingPoint\": {\n        \"globalLocationNumber\": \"SW_CLOTH_1\",\n        \"name\": \"SW Ludwigsburg shipment center\",\n        \"street\": \"Industriestraße 123\",\n        \"postcodeStreet\": \"71634\",\n        \"city\": \"Ludwigsburg\",\n        \"countryISOCode\": \"DE\"\n      },\n      \"material\": {\n        \"identCode\": \"shirt_plain_white\",\n        \"productGroup1Supplier\": \"textiles\",\n        \"productGroup2Supplier\": \"upper_body\",\n        \"shortDescription\": \"Plain white T-Shirt.\",\n        \"size\": \"L\",\n        \"colour\": \"white\"\n      },\n      \"quantitySendBySupplier\": {\n        \"value\": 200,\n        \"quantityUnit\": \"pc\"\n      },\n      \"goodsValue\": {\n        \"value\": 800,\n        \"currencyISOCode\": \"EUR\"\n      }\n    },\n    {\n      \"itemNumber\": \"2\",\n      \"orderItemNumberSupplier\": \"ERP_2851406_2\",\n      \"orderNumberSupplier\": \"ERP_2851406\",\n      \"buyer\": {\n        \"globalLocationNumber\": \"1000\",\n        \"name\": \"FunClothes\",\n        \"street\": \"Haupstraße 405\",\n        \"postcodeStreet\": \"10115\",\n        \"city\": \"Berlin\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"mainoffice@FunClothes.de\"\n      },\n      \"supplier\": {\n        \"globalLocationNumber\": \"SW_CLOTH\",\n        \"name\": \"Swabian Clothes\"\n      },\n      \"consignee\": {\n        \"globalLocationNumber\": \"1000_1\",\n        \"name\": \"FunClothes - Stuttgart location\",\n        \"street\": \"Schlossallee 404\",\n        \"postcodeStreet\": \"70173\",\n        \"city\": \"Stuttgart\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"stuttgart@FunClothes.de\"\n      },\n      \"shippingPoint\": {\n        \"globalLocationNumber\": \"SW_CLOTH_1\",\n        \"name\": \"SW Ludwigsburg shipment center\",\n        \"street\": \"Industriestraße 123\",\n        \"postcodeStreet\": \"71634\",\n        \"city\": \"Ludwigsburg\",\n        \"countryISOCode\": \"DE\"\n      },\n      \"material\": {\n        \"identCode\": \"jeans_blue\",\n        \"productGroup1Supplier\": \"textiles\",\n        \"productGroup2Supplier\": \"lower_body\",\n        \"shortDescription\": \"Plain blue jeans\",\n        \"size\": \"L\",\n        \"colour\": \"blue\"\n      },\n      \"quantitySendBySupplier\": {\n        \"value\": 100,\n        \"quantityUnit\": \"pc\"\n      },\n      \"goodsValue\": {\n        \"value\": 680,\n        \"currencyISOCode\": \"EUR\"\n      }\n    }\n  ],\n  \"transports\": [\n    {\n      \"metaData\": {\n        \"senderID\": \"SwabCloth_ERP\",\n        \"receiverClient\": \"SwabCloth\",\n        \"receiverRole\": \"SUPPLIER\",\n        \"senderRole\": \"SUPPLIER\",\n        \"sendDate\": {\n          \"dateInTimezone\": \"2020-10-10 15:33:34\",\n          \"timezone\": \"Europe/Berlin\"\n        },\n        \"messageReferenceNumber\": \"ERP_2851407_Transport_1\",\n        \"updateMode\": \"STANDARD\",\n        \"idRefScheme\": \"SUPPLIER\"\n      },\n      \"head\": {\n        \"consignmentNumber\": \"ERP_2851406_1\",\n        \"masterWayBillNumber\": \"123456789\",\n        \"plannedDepartureDate\": {\n          \"dateInTimezone\": \"2020-10-10 17:00:00\",\n          \"timezone\": \"Europe/Berlin\"\n        },\n        \"startLoc\": {\n          \"city\": \"Ludwigsburg\",\n          \"countryISOCode\": \"DE\",\n          \"postcodeStreet\": \"71634\",\n          \"timezone\": \"Europe/Berlin\",\n          \"globLocationNo\": \"SW_CLOTH_1\"\n        },\n        \"endLoc\": {\n          \"city\": \"Stuttgart\",\n          \"countryISOCode\": \"DE\",\n          \"postcodeStreet\": \"70173\",\n          \"timezone\": \"Europe/Berlin\",\n          \"globLocationNo\": \"1000_1\"\n        },\n        \"supplier\": {\n          \"globalLocationNumber\": \"SW_CLOTH\",\n          \"name\": \"Swabian Clothes\"\n        },\n        \"globalTransactionNumber\": \"ERP_2851406_1_Transport_1\"\n      }\n    }\n  ]\n}",
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
The call creates a shipment, two shipment items and a transport.

## Search
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3d7c1d2-receiveConsignmentWithTransport_search.PNG",
        "receiveConsignmentWithTransport_search.PNG",
        1258,
        84,
        "#e9e9ea"
      ]
    }
  ]
}
[/block]
## Shipment Navigator
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/954bdf0-receiveConsignmentWithTransport_navigator.PNG",
        "receiveConsignmentWithTransport_navigator.PNG",
        1467,
        301,
        "#f7f7f7"
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
## items
The data for the shipment items is filled here.

It is essential that the `orderNumberSupplier`, `supplier.globalLocationNumber` and the `orderItemNumberSupplier`, like they are filled in the corresponding order item and order, because these fields are used to calculate the reference that connects the shipment item to the order item in the `SUPPLIER` scheme.

More information about id and references calculation can be found at [Object IDs & References](doc:referencing-data-1).

# transport

`masterWayBillNumber` This field is filled with tracking number received from DHL.