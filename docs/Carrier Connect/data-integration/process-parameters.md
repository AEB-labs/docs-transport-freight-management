---
title: Process Parameters
excerpt: >-
  The process parameters for a shipment specify which operations have to be
  performed after a shipment has been created.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

We use different fields to control and influence the operations that Carrier Connect performs with each API call. We call those fields `processParms`. 

<CCOProcessParms />

# processParms in detail

## processMode

API calls can be performed synchronously or asynchronously.

### Process mode "BASIC" - asynchronous

> 📘
>
> In the *asynchronous* communication mode, Carrier Connect checks whether it is generally possible to perform an operation (e.g. check transactionId for uniqueness) and accepts the task if no issues are detected. Only then, more sophisticated validations are performed. 
>
> The calling system only learns about possible warnings by frequently synchronizing with Carrier Connect using the sync calls of the API.

Triggers asynchronous communication. Default mode if nothing else is provided.\
The operation is processed in an asynchronous job after performing some basic checks.

```json
"processParms": {
    "processMode": {
      "mode": "BASIC"
    },
...
```
```xml
<processParms>
     <processMode>
         <mode>BASIC</mode>
     </processMode>
     ...
</processParms>
```

### Process mode "EXTENDED" - synchronous

> 📘
>
> These options are provided to match the shipping context and the technical capabilities of the calling system.\
> *Synchronous* communication responds with more distinct results. No additional lookup to verify the final result of an operation is needed. 
>
> On the other hand, it closely links the calling system with Carrier Connect and sometimes it might be preferable to avoid this.

Triggers synchronous communication.\
The operation is executed directly within the API request transaction and no response is returned until the process is finished.

```json
"processParms": {
    "processMode": {
      "mode": "EXTENDED"
    },
...
```
```xml
<processParms>
     <processMode>
         <mode>EXTENDED</mode>
     </processMode>
     ...
</processParms>
```

> 📘 What is common use?
>
> Most customers prefer the synchronous calls with EXTENDED mode.

## documentPrepareScope and documentOutputScope

The *documentPrepareScope* and *documentOutputScope* are parameters used in Carrier Connect to control the preparation and output of documents, such as labels, and the possible separation of these processes.

The *documentPrepareScope* parameter determines which documents need to be generated or prepared. The possible values for this parameter are:

* `NONE`: No preparation will happen.
* `ALL`: All documents including the already processed ones are considered.
* `REMAINING`: Only the remaining, not yet processed documents are considered.
* `REQUEST`: Only documents for the packages included in the specific API call are considered.
* `SHIPMENTONLY`: No package documents are processed. The shipment (header) is prepared, and all possible calculations like routing data are calculated. This leads to improved performance when package documents are prepared.

The *documentOutputScope* parameter determines the desired output of the documents, the possible values for this parameter are the same as those for the *documentPrepareScope* parameter.

By setting the *documentPrepareScope* and *documentOutputScope* parameters to different values, the user can completely separate the creation of documents from printing them. That means, you could generate documents and request them for printing later. This provides flexibility and optimization for performance and data processing for label printing on package level.

### Example

In the provided example, the `createShipment` API call is used to create a shipment, and the *documentPrepareScope* parameter is set to `SHIPMENTONLY`, indicating that no package documents are generated. The *documentOutputScope* parameter is set to `NONE`, indicating that no output is generated.

```json
"processParms": {
    "documentPrepareScope": {
      "scope": "SHIPMENTONLY"
    },
    "documentOutputScope": {
      "scope": "NONE"
...
  },
```
```xml
<processParms>
     <documentPrepareScope>
         <scope>SHIPMENTONLY</scope>
     </documentPrepareScope>
     <documentOutputScope>
         <scope>NONE</scope>
     </documentOutputScope>
</processParms>
```

In the `processShipment` API call, used to add one or more packages, the *documentPrepareScope* parameter is set to `REQUEST`, indicating that only documents for the packages included in the specific API call are considered. The *documentOutputScope* parameter is also set to `REQUEST`, 

```json
"processParms": {
    "documentPrepareScope": {
      "scope": "REQUEST"
    },
    "documentOutputScope": {
      "scope": "REQUEST"
    },
    "documentOutputMode": {
      "mode": "RETURN"
    },
    "doCompletion": false
  },
```
```xml
<processParms>
     <documentPrepareScope>
         <scope>REQUEST</scope>
     </documentPrepareScope>
     <documentOutputScope>
         <scope>REQUEST</scope>
     </documentOutputScope>
     <documentOutputMode>
         <mode>RETURN</mode>
     </documentOutputMode>
  	 <doCompletion>false</doCompletion>
</processParms>
```

## documentOutputMode

<Callout icon="💡" theme="default">
  ### Find more details in our guide "[Printing with Carrier Connect](https://docs.aeb.com/doc/cm-809258763-823972491-en-US/t-823972491-809258763-en-US)".
</Callout>

The Carrier Connect system provides two output modes for creating and handling documents, such as labels and loading lists: `RETURN` and `PRINT`. Additionally, there is  `NONE` if no output is required.

### RETURN mode

The `RETURN` mode is the preferred mode when working synchronously with the Carrier Connect system. In this mode, all requested documents will be created and returned in the response of the API call. The documents can be retrieved at any time after creation using synchronous API calls. To use the `RETURN` mode, the user needs to set the mode parameter of the documentOutputMode field to `RETURN` in the API call.

```json
"processParms": {
    "documentOutputMode": {
      "mode": "RETURN"
    }
  ...
  },
```
```xml XML
<processParms>
     <documentOutputMode>
         <mode>RETURN</mode>
     </documentOutputMode>
     ...
</processParms>
```

#### Response

The documents generated by Carrier Connect will be returned in `packageResults` > `documents` > `content`.

```json
{
    ...
    "packageResults": [
        {
            "packageTransactionId": "10_8131000_720257_9171",
            "referenceNumber1": "10_8131000_720257_9171",
            "carrierPackageNumber": "1Z4550010450001863",
            "documents": [
                {
                    "documentType": "UPS Label 2017",
                    "mimeType": "application/pdf",
                    "content": ""
                }
            ]
        }
    ],
    ...
}
```
```xml
...
<packageResults>
	<packageResult>
		<packageTransactionId>10_8131000_720257_9171</packageTransactionId>
		<referenceNumber1>10_8131000_720257_9171</referenceNumber1>
		<carrierPackageNumber>1Z4550010450001863</carrierPackageNumber>
		<documents>
			<document>
				<documentType>UPS Label 2017</documentType>
				<mimeType>application/pdf</mimeType>
				<content></content>
			</document>
		</documents>
    </packageResult>
</packageResults>
...
```

### PRINT mode

<Callout icon="💡" theme="default">
  ### Print mode should not be the first choice for printing

  It is important to note, that this mode should not be the first choice for printing, as it can have slower printing performance than the `RETURN` mode, and more information about the printing infrastructure, such as specific printers (not just the type of printers), must be provided in Carrier Connect. There can also be additional costs for the Cloud Printing Agent installation via AEB.
</Callout>

The `PRINT` mode is a special mode designed for cases when the host system has no printing capabilities and works only in connection with an AEB printing agent. In this mode, print jobs are assigned to the workstation ID used in the API call, and the AEB print agent running on the client system responsible for printing constantly polls for print jobs using a specific workstation ID. To use the `PRINT` mode, the user needs to set the mode parameter of the documentOutputMode field to `PRINT` in the API call.

```json
"processParms": {
    "documentOutputMode": {
      "mode": "PRINT"
    }
  ...
  },
```
```xml XML
<processParms>
     <documentOutputMode>
         <mode>PRINT</mode>
     </documentOutputMode>
     ...
</processParms>
```

### NONE mode

The `NONE` output mode in Carrier Connect is used when no output of documents is required. This parameter is independent of the document generation process itself and simply means that no documents will be outputted, even if they were generated.

Using the `NONE` output mode can be useful in complex shipping scenarios, where it is necessary to generate documents ahead of time and request them for printing only at a later stage. This approach can provide more flexibility and control over the printing process, as well as optimizing the performance of the overall system.

```json
"processParms": {
    "documentOutputMode": {
      "mode": "NONE"
    }
  ...
  },
```
```xml XML
<processParms>
     <documentOutputMode>
         <mode>NONE</mode>
     </documentOutputMode>
     ...
</processParms>
```

## workstationId

The API field `workstationId` is a required parameter for most requests in the Carrier Connect system. It is used to identify the specific workstation that is responsible for preparing and printing documents, such as labels, within the system.

In Carrier Connect, workstations are part of the master data that must be set up before they can be used. Each workstation is associated with one or more printers, which are typically used for label printing and laser printing. The output format of the printed documents is determined based on the assigned printers, which may use different formats such as PDF, ZPLII, etc.

![](https://files.readme.io/2bc8f28-image.png)

The `workstationI` parameter is critical to the proper functioning of the Carrier Connect system, as without a valid workstation ID, the system cannot prepare or print any documents. This is because each workstation is responsible for detecting the specific printer for which documents should be prepared and printed.

It is important to note that using an incorrect workstationID can result in errors. For example, if package documents (labels) have already been prepared and are now being printed with a different `workstationI` that has an incompatible printer, an error will be returned. Therefore, it is essential to ensure that the correct `workstationI` is provided when making requests to the Carrier Connect system.

![](https://files.readme.io/ab803cf-Screenshot_2023-02-09_160000.jpg "Screenshot 2023-02-09 160000.jpg")

![](https://files.readme.io/85616ce-Screenshot_2023-02-09_160051.jpg "Screenshot 2023-02-09 160051.jpg")

## doCompletion

The `doCompletion` parameter is a simple `true`/`false` value that indicates whether a shipping order has been completed or whether further operations, such as adding more packages or items, might be needed, and the shipping order therefore has to remain open for another while.

When the doCompletion parameter is set to `true`, it indicates that the shipment has been completed and can no longer be changed via the interface except for canceling it. This means that no additional packages or items can be added to the shipment, and it is ready for pickup or delivery.

Once a shipment has been completed, it can be assigned to pickups if necessary. If a carrier is set up with automatic pickup disposal, all completed shipments will be automatically assigned to a pickup for collection and delivery to their destination.

It is important to note that setting the doCompletion parameter to true should only be done when the shipment is truly completed and no further changes are expected. If additional packages or items need to be added to the shipment, the doCompletion parameter should be set to `false`, indicating that the shipment is not yet completed and further operations are planned.

More information can also be found in the [config guide](https://docs.aeb.com/doc/cm-620065803-801708043-en-US/t-801708043-668622987-en-US)

```json
"processParms": {
    "doCompletion": "true"
...
```
```xml
<processParms>
     <doCompletion>
         <mode>true</mode>
     </doCompletion>
     ...
</processParms>
```

# *processParms* for common use cases

## Use case #1: Complete the shipment and return all labels

You want to return labels for all the contained packages in the shipment and complete the whole shipment afterwards. No more changes are now possible.

```json
"processParms": {
    "processMode": {
        "mode": "EXTENDED"
    },
    "documentPrepareScope": {
        "scope": "ALL"
    },
    "documentOutputScope": {
        "scope": "ALL"
    },
    "documentOutputMode": {
        "mode": "RETURN"
    },
    "doCompletion": true,
    "workstationId": "PDF_WORKSTATION"
}
```
```xml XML
<processParms>
     <processMode>
          <mode>EXTENDED</mode>
     </processMode>
     <documentPrepareScope>
          <scope>ALL</scope>
     </documentPrepareScope>
     <workstationId>PDF_WORKSTATION</workstationId>
     <documentOutputScope>
          <scope>ALL</scope>
     </documentOutputScope>
     <documentOutputMode>
          <mode>RETURN</mode>
     </documentOutputMode>
     <doCompletion>true</doCompletion>
</processParms>
```

## Use case #2: Process only the requested packages, return labels but keep the shipment open

A user wants to return labels in the web service response for all the contained packages in the request. The shipment remains open.

```json
"processParms": {
    "processMode": {
        "mode": "EXTENDED"
    },
    "documentPrepareScope": {
        "scope": "ALL"
    },
    "documentOutputScope": {
        "scope": "REQUEST"
    },
    "documentOutputMode": {
        "mode": "RETURN"
    },
    "doCompletion": false,
    "workstationId": "PDF_WORKSTATION"
}
```
```xml XML
<processParms>
     <processMode>
          <mode>EXTENDED</mode>
     </processMode>
     <documentPrepareScope>
          <scope>ALL</scope>
     </documentPrepareScope>
     <workstationId>PDF_WORKSTATION</workstationId>
     <documentOutputScope>
          <scope>REQUEST</scope>
     </documentOutputScope>
     <documentOutputMode>
          <mode>RETURN</mode>
     </documentOutputMode>
     <doCompletion>false</doCompletion>
</processParms>
```

## Use case #3: Prepare the shipment and calculating routing without package/labels involved

A user wants to prepare the shipment with routing, service area and general carrier checks without any package data or labels involved. These can be added later by another web service call.

```json
"processParms": {
    "processMode": {
        "mode": "BASIC"
    },
    "documentPrepareScope": {
        "scope": "SHIPMENTONLY"
    },
    "workstationId": "PDF_WORKSTATION",
    "documentOutputScope": {
        "scope": "NONE"
    },
    "documentOutputMode": {
        "mode": "NONE"
    },
    "doCompletion": false
},
```
```xml XML
<processParms>
     <processMode>
          <mode>BASIC</mode>
     </processMode>
     <documentPrepareScope>
          <scope>SHIPMENTONLY</scope>
     </documentPrepareScope>
     <workstationId>PDF_WORKSTATION</workstationId>
     <documentOutputScope>
          <scope>NONE</scope>
     </documentOutputScope>
     <documentOutputMode>
          <mode>NONE</mode>
     </documentOutputMode>
     <doCompletion>false</doCompletion>
</processParms>
```
