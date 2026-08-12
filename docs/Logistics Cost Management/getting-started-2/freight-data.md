---
title: Freight data
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
When calling createServiceItems, you can add additional data to your service items ("extendedData"). The additional data of a service item in Logistics Cost Management contains details that are relevant for price calculation and that are specific to the type of service described. Each service type is assigned one additional data type.

Here you can find a description of the fields in the standard freight data:

# BFreightTransportExtendedData

| Variable name              | Type                                                | Comment                                             |
| :------------------------- | :-------------------------------------------------- | :-------------------------------------------------- |
| auxiliaryServiceEntries    | Standard.Collection                                 | Dependent single services of the transport.         |
| carrierValueAddedServices  | Standard.Collection                                 | TSP value-added services of the transport.          |
| exportOrder                | BillingFreightTransport.BExportDeliveryOrderExtData | Customs service of the delivery order.              |
| customsValue               | Billing.BAmountOfMoney                              | Customs value of the delivery order.                |
| isDangerousGoods           | Standard.Boolean                                    |                                                     |
| distance                   | Billing.BQuantity                                   | The distance from transport start to transport end. |
| isDocumentShipment         | Standard.Boolean                                    |                                                     |
| goodsValue                 | Billing.BAmountOfMoney                              | Goods value of the delivery order.                  |
| grossWeight                | Billing.BQuantity                                   | The gross weight of the transport.                  |
| incotermIdentCode          | Standard.String                                     | Incoterms of the delivery order.                    |
| items                      | Standard.Collection                                 | Delivery items of the delivery order.               |
| loadingMeters              | Billing.BQuantity                                   | The loading meters of the transport.                |
| modeOfTransportIdentCode   | Standard.String                                     | The mode of transport.                              |
| numberOfDeliveryNotes      | Standard.Number                                     | Number of delivery notes of the delivery order.     |
| numberOfInvoices           | Standard.Number                                     | Number of invoices of the delivery order.           |
| numberOfItems              | Standard.Number                                     | Number of items of the delivery order.              |
| numberOfPackages           | Standard.Number                                     | Number of packages in transport.                    |
| packages                   | Standard.Collection                                 | Packages of the transport.                          |
| palletPlaces               | Standard.Number                                     | Number of required pallet places of the transport.  |
| referenceNumber            | Standard.String                                     | Reference number of the delivery order.             |
| transportEnd               | LogisticsExtension.AreaAddress                      | Transport end of the transport.                     |
| transportStart             | LogisticsExtension.AreaAddress                      | Transport start of the transport.                   |
| carrierDefinitionIdentCode | Standard.String                                     | TSP abbreviation of the transport.                  |
| volume                     | Billing.BQuantity                                   | The total volume of the transport.                  |

## auxiliaryServiceEntries

| Variable name         | Type                 | Comment                                          |
| :-------------------- | :------------------- | :----------------------------------------------- |
| quantity              | Billing.BQuantity    | Quantity and quantity unit of single service.    |
| singleServiceDate     | Billing.BDateAndZone | Date of service provision of the single service. |
| singleServiceTypeCode | Standard.String      | Ident code of the single service type.           |

## carrierValueAddedServices

| Variable name | Type            | Comment |
| :------------ | :-------------- | :------ |
| identCode     | Standard.String |         |

## exportOrder

| Variable name             | Type                | Comment                                                                 |
| :------------------------ | :------------------ | :---------------------------------------------------------------------- |
| numberOfExportItems       | Standard.Number     | Number of customs items of the delivery order.                          |
| isCustomsHandlingEU       | Standard.Boolean    | Indicates that the delivery order is subject to EU customs processing.  |
| isSubjectToExportControls | Standard.Boolean    | Indicates that the delivery order is subject to export controls.        |
| exportItems               | Standard.Collection | Customs items of the delivery order                                     |
| quantity                  | Billing.BQuantity   | Quantity of the customs item                                            |
| isLetterOfCredit          | Standard.Boolean    | Indicates that the delivery order is processed with a letter of credit. |

### exportItems

| Variable name       | Type            | Comment                            |
| :------------------ | :-------------- | :--------------------------------- |
| customsTariffNumber | Standard.String | Commodity code of the item         |
| procedureCode       | Standard.String | Procedure code of the customs item |

## items

| Variable name     | Type                   | Comment                                                             |
| :---------------- | :--------------------- | :------------------------------------------------------------------ |
| itemNumber        | Standard.String        | Item number of the delivery item.                                   |
| productCode       | Standard.String        | Material number of the delivery item.                               |
| quantity          | Billing.BQuantity      | Quantity of the delivery item.                                      |
| transactionNumber | Standard.String        | Transaction number of the delivery item, e.g. delivery note number. |
| netPrice          | Billing.BAmountOfMoney | Unit net price of the delivery item.                                |
| netWeight         | Billing.BQuantity      | Unit net weight of the delivery item.                               |

## packages

| Variable name              | Type                       | Comment                                                                                                                              |
| :------------------------- | :------------------------- | :----------------------------------------------------------------------------------------------------------------------------------- |
| dangerousGoodsHandlingCode | Standard.String            |                                                                                                                                      |
| dimensions                 | Logistics.CuboidDimensions |                                                                                                                                      |
| numberOfPackages           | Standard.Number            |                                                                                                                                      |
| packageTypeIdentCode       | Standard.String            |                                                                                                                                      |
| packageReferenceNumber     | Standard.String            |                                                                                                                                      |
| grossWeight                | Billing.BQuantity          |                                                                                                                                      |
| volume                     | Billing.BQuantity          |                                                                                                                                      |
| palletPlaces               | Standard.Number            | Number of required pallet places of the transport.                                                                                   |
| referenceNumber            | Standard.String            | Reference number of the delivery order.                                                                                              |
| processingIndicator        | Standard.String            | Indicator that specifies how the handling unit is to be handled during transport, e.g. hanging, vertical, upright, or roll-transport |

## Types

### Billing.BQuantity

| Variable name | Type            | Comment                    |
| :------------ | :-------------- | :------------------------- |
| value         | Standard.Number | Amount of quantity         |
| unit          | Standard.String | Quantity unit abbreviation |

### Billing.BDateAndZone

| Variable name  | Type            | Comment |
| :------------- | :-------------- | :------ |
| dateInTimezone | Standard.String |         |
| timezone       | Standard.String |         |

### Billing.BAmountOfMoney

| Variable name | Type            | Comment                                |
| :------------ | :-------------- | :------------------------------------- |
| value         | Standard.Number | Value of the monetary amount           |
| currencyIso   | Standard.String | Currency of amount of money (ISO code) |

### Logistics.CuboidDimensions

| Variable name | Type            | Comment |
| :------------ | :-------------- | :------ |
| height        | Standard.Number |         |
| length        | Standard.Number |         |
| quantityUnit  | Standard.String |         |
| width         | Standard.Number |         |

### LogisticsExtension.AreaAddress

| Variable name | Type                                 | Comment |
| :------------ | :----------------------------------- | :------ |
| postalAddress | LogisticsExtension.AreaPostalAddress |         |
| locationRef   | LogisticsExtension.AreaLocationRef   |         |

### LogisticsExtension.AreaPostalAddress

| Variable name  | Type            | Comment |
| :------------- | :-------------- | :------ |
| city           | Standard.String |         |
| countryIsoCode | Standard.String |         |
| postcode       | Standard.String |         |
| stateRegion    | Standard.String |         |

### LogisticsExtension.AreaLocationRef

| Variable name | Type            | Comment |
| :------------ | :-------------- | :------ |
| identCode     | Standard.String |         |
| typeId        | Standard.String |         |
