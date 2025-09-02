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
For *Swabian Clothes* everything starts with an <Glossary>Order</Glossary> that is placed in their online shop system by a customer.\
Whenever an order is placed, the shop system creates an entry for the order in their ERP system.

In this example a customer ordered the following items to one of their department stores:

* 200x plain white tshirts
* 100x jeans

each of which is represented by a <Glossary>Order item</Glossary> in M\&A.

## receiveOrder

In this example, every order in the ERP needs to be confirmed by a clerk, before the company starts working on it.\
In this case the order has just been confirmed, now the corresponding data should be sent to the *Monitoring & Alerting* platform.\
To do this the **receiveOrder** function is called:

```json
{
  "metaData": {
    "senderID": "SwabCloth_ERP",
    "receiverClient": "SwabCloth",
    "receiverRole": "SUPPLIER",
    "senderRole": "SUPPLIER",
    "sendDate": {
      "dateInTimezone": "2020-10-10 12:33:34",
      "timezone": "Europe/Berlin"
    },
    "messageReferenceNumber": "ERP_2851406",
    "messageType": "ORDER",
    "updateMode": "STANDARD",
    "idRefScheme": "SUPPLIER"
  },
  "head": {
    "orderType": "New Order - Textiles",
    "orderDateBuyer": {
      "dateInTimezone": "2020-10-10 11:11:34",
      "timezone": "Europe/Berlin"
    },
    "orderNumberSupplier": "ERP_2851406",
    "orderDateSupplier": {
      "dateInTimezone": "2020-10-10 11:12:11",
      "timezone": "Europe/Berlin"
    },
    "latestDeliveryDate": {
      "dateInTimezone": "2020-10-17 11:11:34",
      "timezone": "Europe/Berlin"
    },
    "orderACKDate": {
      "dateInTimezone": "2020-10-10 12:32:44",
      "timezone": "Europe/Berlin"
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
    "seller": {
      "globalLocationNumber": "SW_CLOTH",
      "name": "Swabian Clothes"
    },
    "installationIDHost": "SwabCloth_ERP",
    "dataSourceIDHost": "82149028109"
  },
  "items": [
    {
      "orderItemNumberSupplier": "ERP_2851406_1",
      "orderACKDate": {
        "dateInTimezone": "2020-10-10 12:32:44",
        "timezone": "Europe/Berlin"
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
      "material": {
        "identCode": "shirt_plain_white",
        "productGroup1Supplier": "textiles",
        "productGroup2Supplier": "upper_body",
        "shortDescription": "Plain white T-Shirt.",
        "size": "L",
        "colour": "white"
      },
      "goodsValue": {
        "value": 800,
        "currencyISOCode": "EUR"
      },
      "latestDeliveryDate": {
        "dateInTimezone": "2020-10-17 11:11:34",
        "timezone": "Europe/Berlin"
      },
      "quantityOrdered": {
        "value": 200,
        "quantityUnit": "pc"
      },
      "supplier": {
        "globalLocationNumber": "SW_CLOTH",
        "name": "Swabian Clothes"
      },
      "buyer": {
        "globalLocationNumber": "1000",
        "name": "FunClothes",
        "street": "Haupstraße 405",
        "postcodeStreet": "10115",
        "city": "Berlin",
        "countryISOCode": "DE",
        "timezone": "Europe/Berlin",
        "emailAddress": "mainoffice@FunClothes.de"
      }
    },
    {
      "orderItemNumberSupplier": "ERP_2851406_2",
      "orderACKDate": {
        "dateInTimezone": "2020-10-10 12:32:44",
        "timezone": "Europe/Berlin"
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
      "material": {
        "identCode": "jeans_blue",
        "productGroup1Supplier": "textiles",
        "productGroup2Supplier": "lower_body",
        "shortDescription": "Plain blue jeans.",
        "size": "L",
        "colour": "blue"
      },
      "goodsValue": {
        "value": 680,
        "currencyISOCode": "EUR"
      },
      "latestDeliveryDate": {
        "dateInTimezone": "2020-10-17 11:11:34",
        "timezone": "Europe/Berlin"
      },
      "quantityOrdered": {
        "value": 100,
        "quantityUnit": "pc"
      },
      "supplier": {
        "globalLocationNumber": "SW_CLOTH",
        "name": "Swabian Clothes"
      },
      "buyer": {
        "globalLocationNumber": "1000",
        "name": "FunClothes",
        "street": "Haupstraße 405",
        "postcodeStreet": "10115",
        "city": "Berlin",
        "countryISOCode": "DE",
        "timezone": "Europe/Berlin",
        "emailAddress": "mainoffice@FunClothes.de"
      }
    }
  ]
}
```

## Result

This function call creates an order and two corresponding order items in the system.

## Search

![1258](https://files.readme.io/34bf07f-receiveOrder_-_Order_search.PNG "receiveOrder - Order search.PNG")

## Order Navigator

![1467](https://files.readme.io/a721762-receiveOrder_-_Order_navigator.PNG "receiveOrder - Order navigator.PNG")

## Explanations

This section explains why a specific value was chosen.

## IsWithoutReferenceItem

In this case we set this value to `true`, because we do not want that data from a `reference order item` is copied to the order. We supply every data on each object.

## Metadata

`senderId`: This should be a unique Id for the system that sends the message. In this case this identifies the ERP system of Swabian Clothing.

`receiverClient`: The client name in M\&A is `SwabCloth`.

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

`expectedDeliveryDate`: In this case we do not send this field, because the calculation for this field is done by M\&A automatically. See: [Transit time calculations](doc:dates).

`orderACKDate`: The date at which the clerk confirmed this order.

`installationIDHost`: The Id of the system the data was sent from.

`dataSourceIDHost`: For this we use the database id of the entry in our ERP.

### consignee

We fill this data with the specific departement store that shall receive the order.\
This data is important, for transit time calculations that are done by M\&A.

`globalLocationNumber`: A unique number for the partner, that we take from the ERP.

### buyer

This data is filled with main office location of the ordering company.

## items

This data is filled with the items that are part of the order:

* 200x plain white tshirts
* 100x jeans
