---
title: An order is placed
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
For *Swabian Clothes* everything starts with an <<glossary:Order>> that is placed in their online shop system by a customer. 
Whenever an order is placed, the shop system creates an entry for the order in their ERP system.

In this example a customer ordered the following items to one of their department stores:

  * 200x plain white tshirts
  * 100x jeans

each of which is represented by a <<glossary:Order item>> in M&A.
[block:api-header]
{
  "title": "receiveOrder"
}
[/block]
In this example, every order in the ERP needs to be confirmed by a clerk, before the company starts working on it.
In this case the order has just been confirmed, now the corresponding data should be sent to the *Monitoring & Alerting* platform.
To do this the **receiveOrder** function is called:

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"metaData\": {\n    \"senderID\": \"SwabCloth_ERP\",\n    \"receiverClient\": \"SwabCloth\",\n    \"receiverRole\": \"SUPPLIER\",\n    \"senderRole\": \"SUPPLIER\",\n    \"sendDate\": {\n      \"dateInTimezone\": \"2020-10-10 12:33:34\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"messageReferenceNumber\": \"ERP_2851406\",\n    \"messageType\": \"ORDER\",\n    \"updateMode\": \"STANDARD\",\n    \"idRefScheme\": \"SUPPLIER\"\n  },\n  \"head\": {\n    \"orderType\": \"New Order - Textiles\",\n    \"orderDateBuyer\": {\n      \"dateInTimezone\": \"2020-10-10 11:11:34\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"orderNumberSupplier\": \"ERP_2851406\",\n    \"orderDateSupplier\": {\n      \"dateInTimezone\": \"2020-10-10 11:12:11\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"latestDeliveryDate\": {\n      \"dateInTimezone\": \"2020-10-17 11:11:34\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"orderACKDate\": {\n      \"dateInTimezone\": \"2020-10-10 12:32:44\",\n      \"timezone\": \"Europe/Berlin\"\n    },\n    \"consignee\": {\n      \"globalLocationNumber\": \"1000_1\",\n      \"name\": \"FunClothes - Stuttgart location\",\n      \"street\": \"Schlossallee 404\",\n      \"postcodeStreet\": \"70173\",\n      \"city\": \"Stuttgart\",\n      \"countryISOCode\": \"DE\",\n      \"timezone\": \"Europe/Berlin\",\n      \"emailAddress\": \"stuttgart@FunClothes.de\"\n    },\n    \"buyer\": {\n      \"globalLocationNumber\": \"1000\",\n      \"name\": \"FunClothes\",\n      \"street\": \"Haupstraße 405\",\n      \"postcodeStreet\": \"10115\",\n      \"city\": \"Berlin\",\n      \"countryISOCode\": \"DE\",\n      \"timezone\": \"Europe/Berlin\",\n      \"emailAddress\": \"mainoffice@FunClothes.de\"\n    },\n    \"supplier\": {\n      \"globalLocationNumber\": \"SW_CLOTH\",\n      \"name\": \"Swabian Clothes\"\n    },\n    \"seller\": {\n      \"globalLocationNumber\": \"SW_CLOTH\",\n      \"name\": \"Swabian Clothes\"\n    },\n    \"installationIDHost\": \"SwabCloth_ERP\",\n    \"dataSourceIDHost\": \"82149028109\"\n  },\n  \"items\": [\n    {\n      \"orderItemNumberSupplier\": \"ERP_2851406_1\",\n      \"orderACKDate\": {\n        \"dateInTimezone\": \"2020-10-10 12:32:44\",\n        \"timezone\": \"Europe/Berlin\"\n      },\n      \"consignee\": {\n        \"globalLocationNumber\": \"1000_1\",\n        \"name\": \"FunClothes - Stuttgart location\",\n        \"street\": \"Schlossallee 404\",\n        \"postcodeStreet\": \"70173\",\n        \"city\": \"Stuttgart\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"stuttgart@FunClothes.de\"\n      },\n      \"material\": {\n        \"identCode\": \"shirt_plain_white\",\n        \"productGroup1Supplier\": \"textiles\",\n        \"productGroup2Supplier\": \"upper_body\",\n        \"shortDescription\": \"Plain white T-Shirt.\",\n        \"size\": \"L\",\n        \"colour\": \"white\"\n      },\n      \"goodsValue\": {\n        \"value\": 800,\n        \"currencyISOCode\": \"EUR\"\n      },\n      \"latestDeliveryDate\": {\n        \"dateInTimezone\": \"2020-10-17 11:11:34\",\n        \"timezone\": \"Europe/Berlin\"\n      },\n      \"quantityOrdered\": {\n        \"value\": 200,\n        \"quantityUnit\": \"pc\"\n      },\n      \"supplier\": {\n        \"globalLocationNumber\": \"SW_CLOTH\",\n        \"name\": \"Swabian Clothes\"\n      },\n      \"buyer\": {\n        \"globalLocationNumber\": \"1000\",\n        \"name\": \"FunClothes\",\n        \"street\": \"Haupstraße 405\",\n        \"postcodeStreet\": \"10115\",\n        \"city\": \"Berlin\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"mainoffice@FunClothes.de\"\n      }\n    },\n    {\n      \"orderItemNumberSupplier\": \"ERP_2851406_2\",\n      \"orderACKDate\": {\n        \"dateInTimezone\": \"2020-10-10 12:32:44\",\n        \"timezone\": \"Europe/Berlin\"\n      },\n      \"consignee\": {\n        \"globalLocationNumber\": \"1000_1\",\n        \"name\": \"FunClothes - Stuttgart location\",\n        \"street\": \"Schlossallee 404\",\n        \"postcodeStreet\": \"70173\",\n        \"city\": \"Stuttgart\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"stuttgart@FunClothes.de\"\n      },\n      \"material\": {\n        \"identCode\": \"jeans_blue\",\n        \"productGroup1Supplier\": \"textiles\",\n        \"productGroup2Supplier\": \"lower_body\",\n        \"shortDescription\": \"Plain blue jeans.\",\n        \"size\": \"L\",\n        \"colour\": \"blue\"\n      },\n      \"goodsValue\": {\n        \"value\": 680,\n        \"currencyISOCode\": \"EUR\"\n      },\n      \"latestDeliveryDate\": {\n        \"dateInTimezone\": \"2020-10-17 11:11:34\",\n        \"timezone\": \"Europe/Berlin\"\n      },\n      \"quantityOrdered\": {\n        \"value\": 100,\n        \"quantityUnit\": \"pc\"\n      },\n      \"supplier\": {\n        \"globalLocationNumber\": \"SW_CLOTH\",\n        \"name\": \"Swabian Clothes\"\n      },\n      \"buyer\": {\n        \"globalLocationNumber\": \"1000\",\n        \"name\": \"FunClothes\",\n        \"street\": \"Haupstraße 405\",\n        \"postcodeStreet\": \"10115\",\n        \"city\": \"Berlin\",\n        \"countryISOCode\": \"DE\",\n        \"timezone\": \"Europe/Berlin\",\n        \"emailAddress\": \"mainoffice@FunClothes.de\"\n      }\n    }\n  ]\n}",
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
This function call creates an order and two corresponding order items in the system.

## Search
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/34bf07f-receiveOrder_-_Order_search.PNG",
        "receiveOrder - Order search.PNG",
        1258,
        302,
        "#dce0e3"
      ]
    }
  ]
}
[/block]
## Order Navigator
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a721762-receiveOrder_-_Order_navigator.PNG",
        "receiveOrder - Order navigator.PNG",
        1467,
        528,
        "#ecece7"
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
This section explains why a specific value was chosen.

## IsWithoutReferenceItem
In this case we set this value to `true`, because we do not want that data from a `reference order item` is copied to the order. We supply every data on each object.

## Metadata
`senderId`: This should be a unique Id for the system that sends the message. In this case this identifies the ERP system of Swabian Clothing.

`receiverClient`: The client name in M&A is `SwabCloth`.

`receiverRole` & `senderRole`: Event comes from self and is sent to self, which means we are both the receiver and sender. In this case we supply a customer with clothing which makes us the `SUPPLIER`. See: [Message Metadata](doc:message-metadata#section-receiverrole-senderrole) 

`sendDate`: The date at which the message is sent.

`messageReferenceNumber`: This number is used to identify this message. In this case we simply use the order number from our ERP, which guaranteed to be unique.

`messageType`: Tells us which type of message we are sending. Can be any text.

`updateMode`: Which type of updateMode we want to use. See: [Message Metadata](doc:message-metadata#section-updatemode) 

`idRefScheme`: Calculate the fields like we are the supplier. See: [Object IDs & References](doc:referencing-data-1#section-id-calculation-idrefscheme) 

## Head
`idOrder`: Not used for our idRefScheme

`orderType`: Can be any text, used to search for orders.

`orderDateBuyer`: Time at which the order was placed in the shop system.

`orderNumberSupplier`: The order id taken from the ERP system.

`orderDateSupplier`: The time at which the ERP entry of the order was created.

`latestDeliveryDate`: In this case the customer ordered with *7 day delivery guarantee*, which is why set the latest delivery date to the order date + 7 days.

`expectedDeliveryDate`: In this case we do not send this field, because the calculation for this field is done by M&A automatically. See: [Transit time calculations](doc:dates).

`orderACKDate`: The date at which the clerk confirmed this order.

`installationIDHost`: The Id of the system the data was sent from.

`dataSourceIDHost`: For this we use the database id of the entry in our ERP.

### consignee
We fill this data with the specific departement store that shall receive the order.
This data is important, for transit time calculations that are done by M&A.

`globalLocationNumber`: A unique number for the partner, that we take from the ERP.


### buyer
This data is filled with main office location of the ordering company.

## items
This data is filled with the items that are part of the order:

  * 200x plain white tshirts
  * 100x jeans