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

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        auxiliaryServiceEntries
      </td>

      <td>
        Standard.Collection
      </td>

      <td>
        Dependent single services of the transport.
      </td>
    </tr>

    <tr>
      <td>
        carrierValueAddedServices
      </td>

      <td>
        Standard.Collection
      </td>

      <td>
        TSP value-added services of the transport.
      </td>
    </tr>

    <tr>
      <td>
        exportOrder
      </td>

      <td>
        BillingFreightTransport.BExportDeliveryOrderExtData
      </td>

      <td>
        Customs service of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        customsValue
      </td>

      <td>
        Billing.BAmountOfMoney
      </td>

      <td>
        Customs value of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        isDangerousGoods
      </td>

      <td>
        Standard.Boolean
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        distance
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        The distance from transport start to transport end.
      </td>
    </tr>

    <tr>
      <td>
        isDocumentShipment
      </td>

      <td>
        Standard.Boolean
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        goodsValue
      </td>

      <td>
        Billing.BAmountOfMoney
      </td>

      <td>
        Goods value of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        grossWeight
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        The gross weight of the transport.
      </td>
    </tr>

    <tr>
      <td>
        incotermIdentCode
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Incoterms of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        items
      </td>

      <td>
        Standard.Collection
      </td>

      <td>
        Delivery items of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        loadingMeters
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        The loading meters of the transport.
      </td>
    </tr>

    <tr>
      <td>
        modeOfTransportIdentCode
      </td>

      <td>
        Standard.String
      </td>

      <td>
        The mode of transport.
      </td>
    </tr>

    <tr>
      <td>
        numberOfDeliveryNotes
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of delivery notes of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        numberOfInvoices
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of invoices of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        numberOfItems
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of items of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        numberOfPackages
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of packages in transport.
      </td>
    </tr>

    <tr>
      <td>
        packages
      </td>

      <td>
        Standard.Collection
      </td>

      <td>
        Packages of the transport.
      </td>
    </tr>

    <tr>
      <td>
        palletPlaces
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of required pallet places of the transport.
      </td>
    </tr>

    <tr>
      <td>
        referenceNumber
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Reference number of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        transportEnd
      </td>

      <td>
        LogisticsExtension.AreaAddress
      </td>

      <td>
        Transport end of the transport.
      </td>
    </tr>

    <tr>
      <td>
        transportStart
      </td>

      <td>
        LogisticsExtension.AreaAddress
      </td>

      <td>
        Transport start of the transport.
      </td>
    </tr>

    <tr>
      <td>
        carrierDefinitionIdentCode
      </td>

      <td>
        Standard.String
      </td>

      <td>
        TSP abbreviation of the transport.
      </td>
    </tr>

    <tr>
      <td>
        volume
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        The total volume of the transport.
      </td>
    </tr>
  </tbody>
</Table>

## auxiliaryServiceEntries

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        quantity
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        Quantity and quantity unit of single service.
      </td>
    </tr>

    <tr>
      <td>
        singleServiceDate
      </td>

      <td>
        Billing.BDateAndZone
      </td>

      <td>
        Date of service provision of the single service.
      </td>
    </tr>

    <tr>
      <td>
        singleServiceTypeCode
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Ident code of the single service type.
      </td>
    </tr>
  </tbody>
</Table>

## carrierValueAddedServices

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        identCode
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

## exportOrder

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        numberOfExportItems
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of customs items of the delivery order.
      </td>
    </tr>

    <tr>
      <td>
        isCustomsHandlingEU
      </td>

      <td>
        Standard.Boolean
      </td>

      <td>
        Indicates that the delivery order is subject to EU customs processing.
      </td>
    </tr>

    <tr>
      <td>
        isSubjectToExportControls
      </td>

      <td>
        Standard.Boolean
      </td>

      <td>
        Indicates that the delivery order is subject to export controls.
      </td>
    </tr>

    <tr>
      <td>
        exportItems
      </td>

      <td>
        Standard.Collection
      </td>

      <td>
        Customs items of the delivery order
      </td>
    </tr>

    <tr>
      <td>
        quantity
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        Quantity of the customs item
      </td>
    </tr>

    <tr>
      <td>
        isLetterOfCredit
      </td>

      <td>
        Standard.Boolean
      </td>

      <td>
        Indicates that the delivery order is processed with a letter of credit.
      </td>
    </tr>
  </tbody>
</Table>

### exportItems

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        customsTariffNumber
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Commodity code of the item
      </td>
    </tr>

    <tr>
      <td>
        procedureCode
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Procedure code of the customs item
      </td>
    </tr>
  </tbody>
</Table>

## items

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        itemNumber
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Item number of the delivery item.
      </td>
    </tr>

    <tr>
      <td>
        productCode
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Material number of the delivery item.
      </td>
    </tr>

    <tr>
      <td>
        quantity
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        Quantity of the delivery item.
      </td>
    </tr>

    <tr>
      <td>
        transactionNumber
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Transaction number of the delivery item, e.g. delivery note number.
      </td>
    </tr>

    <tr>
      <td>
        netPrice
      </td>

      <td>
        Billing.BAmountOfMoney
      </td>

      <td>
        Unit net price of the delivery item.
      </td>
    </tr>

    <tr>
      <td>
        netWeight
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>
        Unit net weight of the delivery item.
      </td>
    </tr>
  </tbody>
</Table>

## packages

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        dangerousGoodsHandlingCode
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        dimensions
      </td>

      <td>
        Logistics.CuboidDimensions
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        numberOfPackages
      </td>

      <td>
        Standard.Number
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        packageTypeIdentCode
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        packageReferenceNumber
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        grossWeight
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        volume
      </td>

      <td>
        Billing.BQuantity
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        palletPlaces
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Number of required pallet places of the transport.
      </td>
    </tr>

    <tr>
      <td>
        referenceNumber
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Reference number of the delivery order.
      </td>
    </tr>
  </tbody>
</Table>

## Types

### Billing.BQuantity

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        value
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Amount of quantity
      </td>
    </tr>

    <tr>
      <td>
        unit
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Quantity unit abbreviation
      </td>
    </tr>
  </tbody>
</Table>

### Billing.BDateAndZone

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        dateInTimezone
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        timezone
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

### Billing.BAmountOfMoney

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        value
      </td>

      <td>
        Standard.Number
      </td>

      <td>
        Value of the monetary amount
      </td>
    </tr>

    <tr>
      <td>
        currencyIso
      </td>

      <td>
        Standard.String
      </td>

      <td>
        Currency of amount of money (ISO code)
      </td>
    </tr>
  </tbody>
</Table>

### Logistics.CuboidDimensions

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        height
      </td>

      <td>
        Standard.Number
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        length
      </td>

      <td>
        Standard.Number
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        quantityUnit
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        width
      </td>

      <td>
        Standard.Number
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

### LogisticsExtension.AreaAddress

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        postalAddress
      </td>

      <td>
        LogisticsExtension.AreaPostalAddress
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        locationRef
      </td>

      <td>
        LogisticsExtension.AreaLocationRef
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

### LogisticsExtension.AreaPostalAddress

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        city
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        countryIsoCode
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        postcode
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        stateRegion
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

### LogisticsExtension.AreaLocationRef

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Variable name
      </th>

      <th>
        Type
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        identCode
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        typeId
      </td>

      <td>
        Standard.String
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>
