---
title: Referencing data
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
  pages:
    - type: basic
      slug: create-shipment
      title: Creating a shipment
---
**Referencing shipments**
When creating a shipment, the calling system can provide a *transactionId* and a *referenceNumber1* which can be used to identify the shipment in subsequent API calls.
Whenever a shipment is successfully created, Carrier Connect assigns a *shipmentNumber* to it. This number can be used to identfify the shipment as well.

The *transactionId* (the calling system has to ensure this) and the *shipmentNumber* are always unique within the customer's client setup in Carrier Connect.
Any none-unique *transactionId* will be rejected and result in an error.

The *referenceNumber1* does not have to be unique which makes it a weak reference and it is not recommended to use it as the sole reference.
[block:code]
{
  "codes": [
    {
      "code": " \"shipmentReference\": {\n    \"transactionId\": \"string\",\n    \"referenceNumber1\": \"string\",\n    \"shipmentNumber\": \"string\"\n  }\n",
      "language": "json"
    }
  ]
}
[/block]
**Referencing packages**
Referencing packages is based on the same principles as described above.
Packages can be identified by the *packageTransactionId* which must be unique within the shipment and/or the package's *referenceNumber1*.
To provide the correct context, the shipment containing the package must be referenced as well.
[block:code]
{
  "codes": [
    {
      "code": "\"packageReference\": {\n    \"shipmentReference\": {\n      \"transactionId\": \"string\",\n      \"referenceNumber1\": \"string\",\n      \"shipmentNumber\": \"string\"\n    },\n    \"packageTransactionId\": \"string\",\n    \"referenceNumber1\": \"string\"\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Referencing items**
Items can be identified by the *itemtransactionId* which must be unique within the shipment and/or the item's *referenceNumber1*. These fields are contained in the *shipmentItemReference* structure which also holds a *shipmentReference* to identify the shipment.
The *quantityValue* can be ignored. It is only applied when items are packed into different packages.

[block:code]
{
  "codes": [
    {
      "code": "\"shipmentItemReference\": {\n    \"shipmentReference\": {\n      \"transactionId\": \"string\",\n      \"referenceNumber1\": \"string\",\n      \"shipmentNumber\": \"string\"\n    },\n    \"itemTransactionId\": \"string\",\n    \"referenceNumber1\": \"string\",\n    \"quantityValue\": 0\n}",
      "language": "json"
    }
  ]
}
[/block]