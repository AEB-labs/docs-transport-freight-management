---
title: Delete/Cancel
excerpt: >-
  Learn how to use the Carrier Connect API calls to programmatically DELETE or
  CANCEL existing shipments or pickups.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
[block:html]
{
  "html": "<style>\n  span.cm-s-neo {\n    background-color: #f2f2f2;\n    color: red;\n  }\n</style>"
}
[/block]


# cancelShipment: Cancel a shipping order

With the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/cancelshipment" target="_blank">cancelShipment</a> call you can cancel a <<glossary:shipping order>>. 

> 💡 Please note, that once a shipping order has been completed (i.e.,`doCompletion = true`), it becomes immutable.
> 
> Any data correction is not possible through the interface after completion. Therefore, to make changes, you must first cancel the completed shipping order using the `cancelShipment` call and subsequently retransmit the data with the [createShipment](https://transport-freight-management.docs.developers.aeb.com/reference/createshipment) call.

> ❗️ It's important to highlight, that the `cancelShipment` call sets the shipping order status to _canceled_; the order itself will not be deleted.
> 
> This ensures proper record-keeping while effectively canceling the order.

```json
{
  ...
  "shipmentReference": {
    "referenceNumber1": "1001"
  }
}
```
```xml
...
<shipmentReference>
   <referenceNumber1>1001</referenceNumber1>
</shipmentReference>
...
```

# deleteItem: Delete an item

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/deleteitem" target="_blank">deleteItem</a> call allows you to effectively remove an existing item from a shipping order.

```json
{
  ...
  "shipmentItemReference": {
    "shipmentReference": {
      "referenceNumber1": "1001"
    },
    "itemTransactionId": "YOUR_TRANSACTION_ID"
  }
}
```
```xml
...
<shipmentItemReference>
   <shipmentReference>
      <referenceNumber1>1001</referenceNumber1>
   </shipmentReference>
   <itemTransactionId>YOUR_TRANSACTION_ID</itemTransactionId>
</shipmentItemReference>
```

# deletePackage: Delete a package

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/deletepackage" target="_blank">deletePackage</a> call provides a straightforward method to delete a package from your shipping order.

```json
{
  ...
  "packageReference": {
    "shipmentReference": {
      "referenceNumber1": "1001"
    },
    "packageTransactionId": "YOUR_TRANSACTION_ID"
  }
}
```
```xml
...
<packageReference>
   <shipmentReference>
      <referenceNumber1>1001</referenceNumber1>
   </shipmentReference>
   <packageTransactionId>YOUR_TRANSACTION_ID</packageTransactionId>
</packageReference>
```

# deletePickup: Delete a pickup

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/deletepickup" target="_blank">deletePickup</a> enables you to delete an existing pickup. When this call is made, all shipments associated with the pickup are removed, and they must be assigned to a new pickup using another `createPickup` call. 

> 💡 It's important to note, that a pickup that has already been closed (i.e., `doManifest = true`) cannot be deleted anymore.

```json
{
  ...
  "pickupReference": {
      "referenceNumber1": "1001"
    }
}
```
```xml
...
<pickupReference>
  <referenceNumber1>1001</referenceNumber1>
</pickupReference>
```