---
title: 🚚 Pickup processing
excerpt: ''
deprecated: false
hidden: true
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


Carriers frequently ask for an EDI file at the end of each workday. This file lists all the shipments they've transported. It's crucial for calculating freight costs and planning logistics, such as efficient routing at the carrier's hub.

In Carrier Connect, this is termed as <<glossary:pickup>>. A pickup may include one or several shipping orders.

> 💡 Which option should be chosen when?
> 
> There are multiple options how to create and process the pickup: 
> 
> - If you create objects like loading units in your ERP or have some load control process in place, the best option is to connect the physical goods issue to the pickup creation in Carrier Connect **Automatically via API**. 
> - If you cannot find a good trigger for the pickup creation in ERP, you might have to go for the option **Automatically after 6 hours** or **Manually via user interface in Carrier Connect**.

As soon as you decided for one option, make sure the carrier configurations are set accordingly:  
<a href="https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#667079819667081355" target="_blank">Configuring or generating pickups</a> 

# Automatically via API

Ensure shipping orders are closed before assigning them to a pickup. If working via API and your shipping orders aren't closed yet, see [processShipment](doc:process#processShipment).

## Pickup creation

Use the [createPickup](doc:create#createPickup) method to generate pickups for specific carriers within Carrier Connect. The usage varies based on the parameters set in creationParms and [processParms](doc:processparms).

- **Complete pickup handling**: This includes pickup creation, shipment assignment, printing collection documents (loading lists), EDI sending (if required), completion.
- **Partial pickup processing**: Only creation of a pickup and assignment of the shipments. Shipments can then be added via API ([processPickup](doc:process#update-a-pickup-with-processpickup)) or GUI.  
  Note: removing shipments must be done manually, as there's no API function for this.

To create a pickup, use `transactionId` or `referenceNumber1`: 

```json
{
  "transactionId": "pickup-transactionId",
  "referenceNumber1": "pickup-referenceNumber1",
}
```
```xml
<transactionId>pickup-transactionId</transactionId>
<referenceNumber1>pickup-referenceNumber1</referenceNumber1>
```

For referencing shipments within the pickup, use either `transactionId`, `referenceNumber1` or `shipmentNumber`:

```json JSON
{
  "shipments":[ 
    {
    "transactionId": "shipment-transactionId",
    "referenceNumber1": "shipment-referenceNumber1",
    "shipmentNumber": "shipment-shipmentNumber"
  	}
	]
}
```
```xml
<shipments>
  <transactionId>shipment-transactionId</transactionId>
  <referenceNumber1>shipment-referenceNumber1</referenceNumber1>
  <shipmentNumber>shipment-shipmentNumber</shipmentNumber>
</shipments>
```

## Pickup processing

To modify an existing pickup, use the [processPickup](doc:process#update-a-pickup-with-processpickup) method.

This allows for the completion of partially handled pickups, including printing documents and sending EDI through Carrier Connect. Appropriate parameters should be set in the [processParms](doc:processparms).

To identify an existing pickup, use either the `transactionId`, `referenceNumber1` or `pickupNumber`:

```json JSON
{
  "pickupReference": {
    "transactionId": "pickup-transactionId",
    "referenceNumber1": "pickup-referenceNumber1",
    "pickupNumber": "pickup-shipmentNumber"
  },
```
```xml
<pickupReference>
  <transactionId>pickup-transactionId</transactionId>
  <referenceNumber1>pickup-referenceNumber1</referenceNumber1>
  <pickupNumber>pickup-shipmentNumber</pickupNumber>
</pickupReference>
```

For referencing shipments within the pickup, use either `transactionId`, `referenceNumber1` or `shipmentNumber`:

```json JSON
{
  "shipments":[ 
    {
      "referenceNumber1": "shipment-referenceNumber1",
      ...
      "referenceNumber1": "shipment-referenceNumberN",
  	}
	]
}
```
```xml
<shipments>
    <referenceNumber1>shipment-referenceNumber1</referenceNumber1>
  ...
    <referenceNumber1>shipment-referenceNumberN</referenceNumber1>
</shipments>
```

Key processing and response parameters are: 

- `doManifest`: A flag indicating pickup completion.
- `documentOutputMode`: This parameter determines if existing loading lists should be printed or returned in the response.

```json JSON
{
  "processParms": {
    "doManifest": true,
    "documentOutputMode": {
      "mode": "RETURN"
    },
    "workstationId": "OFFICE2"
  }
}
```
```xml
<processParms>
	<doManifest>true</doManifest>
	<documentOutputMode>
		<mode>RETURN</mode>
	</documentOutputMode>
	<workstationId>OFFICE2</workstationId>
</processParms>
```

# Automatically after 6 hours

Have a look into our configuration and user guide:  
<a href="https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/667079819667081355.html" target="_blank">Section "Configuring automatic pickup completion"</a>

# Manually via user interface in Carrier Connect

Creating and processing pickups manually is described in our configuration and user guide:  
<a href="https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/673513867673515403.html" target="_blank">Assigning shipping orders to pickups manually</a>

> 📘 EDI: Pickup Level vs. Shipment Level
> 
> Carriers vary in how they handle EDI transmissions:
> 
> - **Shipment Level**: For some carriers, the EDI is transmitted at the individual shipping order level. This means the EDI message is often sent when a shipping order is finalized, or in some instances, even earlier. The EDI at the pickup level may then be skipped.
> 
> However, a hybrid approach can exist:
> 
> - **Mixed Scenario**: Here, the EDI sent at the shipment level acts as a notification. Meanwhile, the EDI transmitted at the pickup level serves as a confirmation of all the day's shipping orders.