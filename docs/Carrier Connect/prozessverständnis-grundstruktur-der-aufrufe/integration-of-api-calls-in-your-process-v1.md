---
title: ↪️Integration of API calls in your process (OLD)
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


# Which API calls are the most important?

The most important API calls are:

## Shipment level

- `createShipment`: creates your shipment within Carrier Connect - you cannot work without this call. For more info see [🌱 Create](doc:create).
- `processShipment`: changes, processes or expands your existing shipment. For more info see [🔄 Update](doc:process).
- `cancelShipment`: deletes the shipment (can only be done before closing the pickup). For more info see [🗑️ Delete/Cancel](doc:deletecancel).
- `addShipmentAttachments`: adds files to your existing shipment (required for paperless trade process). For more info see [📤 Attach and upload documents to transmit them to the carrier](doc:transmitting-documents-to-carrier-connect).

## Pickup level

- `createPickup`: creates a pickup of your named shipments, they are gathered into one pickup.

For further information and the whole overview of all the webservice calls, please consider the [API Reference](https://transport-freight-management.docs.developers.aeb.com/docs/processparms).

<br />

# Why would you need different calls for a shipment?

You don't necessarily need all of these calls. Typically, EU-shipments and shipments within a country can be processed with a single `createShipment` call. 

The reasons to understand why it makes sense to use a processShipment are explained within the most important milestones for a shipment:

- creation: the shipment is created
- preparing labels: the labels would be generated and available for printing
- printing labels: the labels are physically printed
- closing shipment: no more changes can be done to this shipment, except canceling.

If these milestones all end up at the same point in time, there is no need to add further calls to your process. 

There are a few questions you should consider before implementing the integration: 

- Will you have shipments with more than 1 package (multi-package-shipments)?  
  In case you have multi-package-shipments: 
  - Do you want to print all labels for all packages at once? 
  - Or do you want to process step by step and print the label directly once a package is packed and weight and dimensions are available.
- Will specific data, such as the customs value or MRN, be available later in the process? Is it before or after the point in time, when you would like to print labels?

# Simple shipping

For example, a shipment can be created via createShipment with all the necessary data. If you set the processParms like this, you will close the shipment at the same time of creating it (all milestones for a shipment are completed at the same time):

`documentPrepareScope=all`  
`documentOutputScope=all`  
`doCompletion=true`  
This is typically done for EU/national shipments. 

![](https://files.readme.io/5b31a8d142a5f49df9d3d415afd8fdf2f7ff2cfd5bcfca98eb7052e882b68faa-hostsystem_cco_simple_EN.png)

<br />

# Advanced Shipping with package-by-package-handling

A typical usecase for a process that is a bit more complex would be this scenario.

You have all the information at once, but you want to print the labels for each package after another. Once a package has been packed, the label should be printed. Then the next package will be packed with the items and once that is full the next label should be printed. 

Therefore, your milestones would look like this: 

createShipment with first package label being printed  
processShipment for the next packages until all items are packed.  
In this case you should set the processParms like this (For more information on the processParms have a look here.): 

createShipment: 

`documentPrepareScope=request`  
`documentOutputScope=request`  
`doCompletion=false`

processShipment: (any package that is not the last of the shipment):

`documentPrepareScope=request`  
`documentOutputScope=request`  
`doCompletion=false`

processShipment: (the last package of the shipment):

`documentPrepareScope=request`  
`documentOutputScope=request`  
`doCompletion=true`

You could also vary this process by developing a processShipment call that only adds and prints the packages and then afterwards using a different user exit for completing the shipment. Therefore, after your last label is printed, you would only send a processShipment that sets the doCompletion on true. 

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


# Advanced Shipping with paperless trade process

There are multiple options to include the paperless trade option that many carriers nowadays ask for. 

There are certain aspects to consider when it comes to including paperless trade in your process. 

This process is only necessary for shipments that need export declarations. Therefore you need to make sure, that only these shipments are using that specific process.  
Paperless trade means, that the export accompanying document and the invoice (pro-forma invoice or commercial invoice) need to be electronically transmitted to the carrier via Carrier Connect.  
These documents need to be added to the Carrier Connect shipment before setting the milestone "close shipment" aka "doCompletion =true".  
Besides the documents, specific information regarding the export must be provided, such as MRN, invoice number, customs value, customs tariffs numbers and some more (see Help Center).  
some of this information (e.g. on item-level) cannot be added via the processShipment but must be updated via updateCustomsData - hopefully you can just transmit most of the information with the initial createShipment.  
If you cannot add the documents via addShipmentAttachments, you could also manually upload them, however, this is not recommended.  
You can integrate the print label by label process, if necessary. Please see the upper version on how to change the parameters then.

![](https://files.readme.io/3148b6c5bae7710bfe51cf61b0f086029bc13c1374c88db0216dffa2bce8dfc2-hostsystem_cco_export_PLT_Processs_EN.png)