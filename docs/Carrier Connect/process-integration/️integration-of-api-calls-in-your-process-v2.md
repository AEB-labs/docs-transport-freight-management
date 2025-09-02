---
title: Integration of API calls in your process
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
[block:html]
{
  "html": "<style>\n  span.cm-s-neo {\n    background-color: #f2f2f2;\n    color: red;\n  }\n</style>"
}
[/block]


<br />

# Which API calls are the most important?

When working with Carrier Connect, certain API calls are fundamental to processing shipments efficiently. Below is an overview of the most important API calls categorized by shipment and pickup levels.

## Shipment-Level API Calls

| API Call                 | Function                                  | Key Notes                                                                                                                                                                |
| :----------------------- | :---------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `createShipment`         | Creates a shipment in Carrier Connect.    | Mandatory for all processes. For more info see [🌱 Create](doc:create).                                                                                                  |
| `processShipment`        | Modifies, updates, or expands a shipment. | Used in multi-step processes. Changes, processes or expands your existing shipment. For more info see [🔄 Update](doc:process).                                          |
| `cancelShipment`         | Deletes the shipment.                     | Only possible before closing the pickup. For more info see [🗑️ Delete/Cancel](doc:deletecancel).                                                                        |
| `addShipmentAttachments` | Adds documents to your existing shipment. | Required for paperless trade process. For more info see [📤 Attach and upload documents to transmit them to the carrier](doc:transmitting-documents-to-carrier-connect). |

## Pickup-Level API Calls

| API Call       | Function                                       | Key Notes                                  |
| :------------- | :--------------------------------------------- | :----------------------------------------- |
| `createPickup` | Creates a pickup which contains _n_ shipments. | For more info see [🌱 Create](doc:create). |

For further information and the whole overview of all the webservice calls, please consider the [API Reference](https://transport-freight-management.docs.developers.aeb.com/docs/processparms).

# Why use different API calls for a shipment?

Not all API calls are required for every shipment. In many cases, a single `createShipment` call is sufficient, especially for domestic and EU shipments.

However, more complex workflows need additional API calls. The key milestones for a shipment are:

- **Creation**– The shipment is created.
- **Label Preparation** – Labels are generated and ready for printing.
- **Label Printing** – Labels are physically printed.
- **Shipment Closure** – The shipment is finalized; no further changes allowed (except cancellation).

If all these steps occur simultaneously, additional API calls are unnecessary. Otherwise, `processShipment` calls will be needed to handle changes incrementally.

## Key Questions for the implementation

- Do you ship multi-package shipments?
  - Print all labels at once? -> [Simple Shipping](https://transport-freight-management.docs.developers.aeb.com/docs/%EF%B8%8Fintegration-of-api-calls-in-your-process-copy#simple-shipping-one-step-process)  
  - Print each package label individually as soon as it's packed? -> [Advanced Shipping with package-by-package-handling](https://transport-freight-management.docs.developers.aeb.com/docs/%EF%B8%8Fintegration-of-api-calls-in-your-process-copy#advanced-shipping-with-package-by-package-handling) 
- Is customs information (e.g., MRN, invoice value) available later in the process?
  - If so, before or after label printing?

# How to Structure Your Shipment Process

Now that you understand the most important API calls, let’s look at different possibilities to integrate your shipment process. The right approach depends on your specific workflow.

## Simple shipping: One-Step Process

For most EU/national shipments, you can create and complete the shipment in one step using `createShipment` with the following settings:

```json
"processParms": {
    "doCompletion": true,
    "documentPrepareScope": {
        "scope": "ALL"
    },
    "documentOutputScope": {
        "scope": "ALL"
    },
    ...
}
```
```xml
<processParms>
	<doCompletion>true</doCompletion>
	<documentPrepareScope>
		<scope>ALL</scope>
	</documentPrepareScope>
	<documentOutputScope>
		<scope>ALL</scope>
	</documentOutputScope>
  ...
</processParms>
```

<br />

![](https://files.readme.io/5b31a8d142a5f49df9d3d415afd8fdf2f7ff2cfd5bcfca98eb7052e882b68faa-hostsystem_cco_simple_EN.png)

<br />

## Advanced Shipping with package-by-package-handling

A typical usecase for a process that is a bit more complex would be this scenario.

You have all the information at once, but you want to print the labels for each package after another. Once a package has been packed, the label should be printed. Then the next package will be packed with the items and once that is full the next label should be printed. 

Therefore, your milestones would look like this: 

createShipment with first package label being printed  
processShipment for the next packages until all items are packed.  
In this case you should set the processParms like this (For more information on the processParms have a look here.): 

`createShipment`:

```json
"processParms": {
    "doCompletion": false,
    "documentPrepareScope": {
        "scope": "REQUEST"
    },
    "documentOutputScope": {
        "scope": "REQUEST"
    },
    ...
}
```
```xml
<processParms>
	<doCompletion>false</doCompletion>
	<documentPrepareScope>
		<scope>REQUEST</scope>
	</documentPrepareScope>
	<documentOutputScope>
		<scope>REQUEST</scope>
	</documentOutputScope>
  ...
</processParms>
```

`processShipment` (any package that is not the last of the shipment):

```json
"processParms": {
    "doCompletion": false,
    "documentPrepareScope": {
        "scope": "REQUEST"
    },
    "documentOutputScope": {
        "scope": "REQUEST"
    },
    ...
}
```
```xml
<processParms>
	<doCompletion>false</doCompletion>
	<documentPrepareScope>
		<scope>REQUEST</scope>
	</documentPrepareScope>
	<documentOutputScope>
		<scope>REQUEST</scope>
	</documentOutputScope>
  ...
</processParms>
```

`processShipment` (the last package of the shipment):

```json
"processParms": {
    "doCompletion": true,
    "documentPrepareScope": {
        "scope": "REQUEST"
    },
    "documentOutputScope": {
        "scope": "REQUEST"
    },
    ...
}
```
```xml
<processParms>
	<doCompletion>true</doCompletion>
	<documentPrepareScope>
		<scope>REQUEST</scope>
	</documentPrepareScope>
	<documentOutputScope>
		<scope>REQUEST</scope>
	</documentOutputScope>
  ...
</processParms>
```

<br />

You could also vary this process by developing a `processShipment` call that only adds and prints the packages and then afterwards using a different user exit for completing the shipment. Therefore, after your last label is printed, you would only send a processShipment that sets the doCompletion on true. 

As you can see, there are various options for integrating and fully automating your processes with Carrier Connect.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4874df5f7f759ddf11b383bebf2e9bb78b7752b690a8735b2df17329567c71f8-hostsystem_cco_packbypack_EN.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


## Advanced Shipping with paperless trade process

There are multiple options to include the paperless trade option that many carriers nowadays ask for. 

There are certain aspects to consider when it comes to including paperless trade in your process. 

This process is only necessary for shipments that need export declarations. Therefore you need to make sure, that only these shipments are using that specific process.  
Paperless trade means, that the export accompanying document and the invoice (pro-forma invoice or commercial invoice) need to be electronically transmitted to the carrier via Carrier Connect.  
These documents need to be added to the Carrier Connect shipment before setting the milestone "close shipment" aka "doCompletion =true".  
Besides the documents, specific information regarding the export must be provided, such as MRN, invoice number, customs value, customs tariffs numbers and some more (see Help Center).

Some of this information (e.g. on item-level) cannot be added via the `processShipment` but must be updated via `updateCustomsData` (For more details have a look [here](https://transport-freight-management.docs.developers.aeb.com/docs/process#updatecustomsdata-update-customs-data)) - hopefully you can just transmit most of the information with the initial `createShipment`.  
If you cannot add the documents via `addShipmentAttachments`, you could also manually upload them, however, this is not recommended.  
You can integrate the print label by label process, if necessary. Please see the upper version on how to change the parameters then.

![](https://files.readme.io/3148b6c5bae7710bfe51cf61b0f086029bc13c1374c88db0216dffa2bce8dfc2-hostsystem_cco_export_PLT_Processs_EN.png)