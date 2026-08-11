---
title: Get to know the Object Model
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
You have now a basic understanding of _Carrier Connect_ – let's have a closer look at the objects the system uses.

<Image align="center" src="https://files.readme.io/d146a7c86e8578e0386954cbc488f4e2452af1fffa9ac59dff105c02dd9ba889-Get_Started_Carrier_Connect_JWA_-_Object_Model.jpg" />

## Shipping order

A shipping order is called `shipment` in the API. It has four data structures:

| Concept                  | In the API                                          | Contains                                                                                                                                                              |
| :----------------------- | :-------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Head**                 | fields directly on `shipment`                       | Header data of the shipping order: shipper (`shippingPt`) and recipient (`consignee`) of the shipment, and the handling conditions.                                    |
| **Packages**             | `shipment.packages[]`                               | The packages to be shipped — dimensions, weight.                                                                                                                      |
| **Items**                | `shipment.items[]`                                  | The items shipped in the shipment — value and quantity. Items can be packed in packages, so the relationship between items and packages is n:m.                        |
| **Carrier and service**  | `shipment.carrierIdentCode`, `shipment.serviceCode` | The selected shipping option. The carrier is automatically derived from the selected service code and is returned as part of the response.                             |

Two identifiers you supply are worth knowing before your first call:

* **`shipment.transactionId`** — your unique reference to the business transaction in your system. _Carrier Connect_ rejects a second shipping order with the same `transactionId`, which is also what makes retries safe. See [Carrier Connect API Essentials](doc:start-here-carrier-connect-api-essentials).
* **`clientSystemId`** — sits on the request, not on the shipment, and identifies the sending host or ERP system (e.g. its installation ID). Set it when more than one system feeds the same _Carrier Connect_ client, so shipping orders stay attributable to their source.

## Pickup

When shipping orders are completed, they are bundled into so-called pickups. When a pickup is complete, the configured documents, such as the manifest, are generated as a PDF and made available to the source system via API. At the same time as the pickup is completed, the shipping orders data is sent to the carrier via EDI or webservice.

Pickups have their own operations: `createPickup`, `processPickup`, `getPickups`, `syncPickups`, `deletePickup`.
