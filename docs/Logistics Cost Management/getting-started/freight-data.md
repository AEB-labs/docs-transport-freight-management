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

#BFreightTransportExtendedData
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "1-0": "carrierValueAddedServices",
    "1-1": "Standard.Collection",
    "1-2": "TSP value-added services of the transport.",
    "0-0": "auxiliaryServiceEntries",
    "0-1": "Standard.Collection",
    "0-2": "Dependent single services of the transport.",
    "2-0": "exportOrder",
    "2-1": "BillingFreightTransport.BExportDeliveryOrderExtData",
    "2-2": "Customs service of the delivery order.",
    "3-0": "customsValue",
    "3-1": "Billing.BAmountOfMoney",
    "3-2": "Customs value of the delivery order.",
    "4-0": "isDangerousGoods",
    "4-1": "Standard.Boolean",
    "5-0": "distance",
    "5-1": "Billing.BQuantity",
    "5-2": "The distance from transport start to transport end.",
    "6-0": "isDocumentShipment",
    "6-1": "Standard.Boolean",
    "7-0": "goodsValue",
    "7-1": "Billing.BAmountOfMoney",
    "7-2": "Goods value of the delivery order.",
    "8-0": "grossWeight",
    "8-1": "Billing.BQuantity",
    "8-2": "The gross weight of the transport.",
    "9-0": "incotermIdentCode",
    "9-1": "Standard.String",
    "9-2": "Incoterms of the delivery order.",
    "10-0": "items",
    "10-1": "Standard.Collection",
    "10-2": "Delivery items of the delivery order.",
    "11-0": "loadingMeters",
    "11-1": "Billing.BQuantity",
    "11-2": "The loading meters of the transport.",
    "12-0": "modeOfTransportIdentCode",
    "12-1": "Standard.String",
    "12-2": "The mode of transport.",
    "13-0": "numberOfDeliveryNotes",
    "13-1": "Standard.Number",
    "13-2": "Number of delivery notes of the delivery order.",
    "14-0": "numberOfInvoices",
    "14-1": "Standard.Number",
    "14-2": "Number of invoices of the delivery order.",
    "15-0": "numberOfItems",
    "15-1": "Standard.Number",
    "15-2": "Number of items of the delivery order.",
    "16-0": "numberOfPackages",
    "16-1": "Standard.Number",
    "16-2": "Number of packages in transport.",
    "17-0": "packages",
    "17-1": "Standard.Collection",
    "17-2": "Packages of the transport.",
    "18-0": "palletPlaces",
    "18-1": "Standard.Number",
    "18-2": "Number of required pallet places of the transport.",
    "19-0": "referenceNumber",
    "19-1": "Standard.String",
    "19-2": "Reference number of the delivery order.",
    "20-0": "transportEnd",
    "20-1": "LogisticsExtension.AreaAddress",
    "20-2": "Transport end of the transport.",
    "21-0": "transportStart",
    "21-1": "LogisticsExtension.AreaAddress",
    "21-2": "Transport start of the transport.",
    "22-0": "carrierDefinitionIdentCode",
    "22-1": "Standard.String",
    "22-2": "TSP abbreviation of the transport.",
    "23-0": "volume",
    "23-1": "Billing.BQuantity",
    "23-2": "The total volume of the transport."
  },
  "cols": 3,
  "rows": 24
}
[/block]
##auxiliaryServiceEntries
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "quantity",
    "0-1": "Billing.BQuantity",
    "0-2": "Quantity and quantity unit of single service.",
    "1-0": "singleServiceDate",
    "1-1": "Billing.BDateAndZone",
    "1-2": "Date of service provision of the single service.",
    "2-0": "singleServiceTypeCode",
    "2-1": "Standard.String",
    "2-2": "Ident code of the single service type."
  },
  "cols": 3,
  "rows": 3
}
[/block]
##carrierValueAddedServices
[block:parameters]
{
  "data": {
    "0-0": "identCode",
    "0-1": "Standard.String",
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment"
  },
  "cols": 3,
  "rows": 1
}
[/block]
##exportOrder
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "numberOfExportItems",
    "0-1": "Standard.Number",
    "0-2": "Number of customs items of the delivery order.",
    "1-0": "isCustomsHandlingEU",
    "1-1": "Standard.Boolean",
    "1-2": "Indicates that the delivery order is subject to EU customs processing.",
    "2-0": "isSubjectToExportControls",
    "2-1": "Standard.Boolean",
    "2-2": "Indicates that the delivery order is subject to export controls.",
    "3-0": "exportItems",
    "3-1": "Standard.Collection",
    "3-2": "Customs items of the delivery order",
    "4-0": "quantity",
    "4-1": "Billing.BQuantity",
    "4-2": "Quantity of the customs item",
    "5-0": "isLetterOfCredit",
    "5-1": "Standard.Boolean",
    "5-2": "Indicates that the delivery order is processed with a letter of credit."
  },
  "cols": 3,
  "rows": 6
}
[/block]
###exportItems
[block:parameters]
{
  "data": {
    "0-0": "customsTariffNumber",
    "0-1": "Standard.String",
    "0-2": "Commodity code of the item",
    "1-0": "procedureCode",
    "1-1": "Standard.String",
    "1-2": "Procedure code of the customs item",
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment"
  },
  "cols": 3,
  "rows": 2
}
[/block]
##items
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "itemNumber",
    "0-1": "Standard.String",
    "0-2": "Item number of the delivery item.",
    "1-0": "productCode",
    "1-1": "Standard.String",
    "1-2": "Material number of the delivery item.",
    "2-0": "quantity",
    "2-1": "Billing.BQuantity",
    "2-2": "Quantity of the delivery item.",
    "3-0": "transactionNumber",
    "3-1": "Standard.String",
    "3-2": "Transaction number of the delivery item, e.g. delivery note number.",
    "4-0": "netPrice",
    "4-1": "Billing.BAmountOfMoney",
    "5-0": "netWeight",
    "4-2": "Unit net price of the delivery item.",
    "5-2": "Unit net weight of the delivery item.",
    "5-1": "Billing.BQuantity"
  },
  "cols": 3,
  "rows": 6
}
[/block]
##packages
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "dangerousGoodsHandlingCode",
    "0-1": "Standard.String",
    "1-0": "dimensions",
    "1-1": "Logistics.CuboidDimensions",
    "2-0": "numberOfPackages",
    "2-1": "Standard.Number",
    "3-0": "packageTypeIdentCode",
    "3-1": "Standard.String",
    "4-0": "packageReferenceNumber",
    "4-1": "Standard.String",
    "5-0": "grossWeight",
    "5-1": "Billing.BQuantity",
    "6-0": "volume",
    "6-1": "Billing.BQuantity",
    "7-0": "palletPlaces",
    "7-1": "Standard.Number",
    "7-2": "Number of required pallet places of the transport.",
    "8-0": "referenceNumber",
    "8-1": "Standard.String",
    "8-2": "Reference number of the delivery order."
  },
  "cols": 3,
  "rows": 9
}
[/block]
##Types

###Billing.BQuantity
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "value",
    "0-1": "Standard.Number",
    "0-2": "Amount of quantity",
    "1-0": "unit",
    "1-1": "Standard.String",
    "1-2": "Quantity unit abbreviation"
  },
  "cols": 3,
  "rows": 2
}
[/block]
###Billing.BDateAndZone
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "dateInTimezone",
    "1-0": "timezone",
    "0-1": "Standard.String",
    "1-1": "Standard.String"
  },
  "cols": 3,
  "rows": 2
}
[/block]
###Billing.BAmountOfMoney
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "value",
    "0-1": "Standard.Number",
    "0-2": "Value of the monetary amount",
    "1-0": "currencyIso",
    "1-1": "Standard.String",
    "1-2": "Currency of amount of money (ISO code)"
  },
  "cols": 3,
  "rows": 2
}
[/block]
###Logistics.CuboidDimensions
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "height",
    "1-0": "length",
    "3-0": "width",
    "0-1": "Standard.Number",
    "1-1": "Standard.Number",
    "3-1": "Standard.Number",
    "2-0": "quantityUnit",
    "2-1": "Standard.String"
  },
  "cols": 3,
  "rows": 4
}
[/block]
###LogisticsExtension.AreaAddress
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "postalAddress",
    "0-1": "LogisticsExtension.AreaPostalAddress",
    "1-0": "locationRef",
    "1-1": "LogisticsExtension.AreaLocationRef"
  },
  "cols": 3,
  "rows": 2
}
[/block]
###LogisticsExtension.AreaPostalAddress
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "city",
    "1-0": "countryIsoCode",
    "2-0": "postcode",
    "3-0": "stateRegion",
    "0-1": "Standard.String",
    "1-1": "Standard.String",
    "2-1": "Standard.String",
    "3-1": "Standard.String"
  },
  "cols": 3,
  "rows": 4
}
[/block]
###LogisticsExtension.AreaLocationRef
[block:parameters]
{
  "data": {
    "h-0": "Variable name",
    "h-1": "Type",
    "h-2": "Comment",
    "0-0": "identCode",
    "1-0": "typeId",
    "0-1": "Standard.String",
    "1-1": "Standard.String"
  },
  "cols": 3,
  "rows": 2
}
[/block]