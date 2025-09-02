---
title: Steering workflow, data preparation, and printing
excerpt: Introduction to creation and process pParameters
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
      slug: data-validation-and-error-handling-1
      title: Data validation and error handling
---
In addition to the business data like shipments, packages, and items, more information is needed to steer the workflow, prepare the correct data, print it at the right time in the right way, and finally know when everything is done.

In most API calls, there are basically two kinds of *parameter sets*' to provide the necessary information:

## CreationParms

See [here](doc:data-validation-and-error-handling) for a detailed explanation.

```json
"creationParms": {
    "creationMode": "string"
  },
```
```xml
<creationParms>
      <creationMode>?</creationMode>
 </creationParms>
```

## ProcessParms

Explantions for [processMode](doc:process-mode), [prepare and output scopes](doc:prepare-and-output-scope) and [output mode](doc:printing-modes) are available in the "Basic concepts" section.

```json
"processParms": {
    "processMode": {
      "mode": "string"
    },
    "documentPrepareScope": {
      "scope": "string"
    },
    "workstationId": "string",
    "documentOutputScope": {
      "scope": "string"
    },
    "documentOutputMode": {
      "mode": "string"
    },
    "doCompletion": true
  },
```
```xml
<processParms>
     <processMode>
          <mode>?</mode>
     </processMode>
     <documentPrepareScope>
          <scope>?</scope>
     </documentPrepareScope>
     <workstationId>?</workstationId>
     <documentOutputScope>
         <scope>?</scope>
     </documentOutputScope>
     <documentOutputMode>
         <mode>?</mode>
     </documentOutputMode>
     <doCompletion>?</doCompletion>
</processParms>
```

## Workstation ID

Most of the requests require a *Workstation ID*.\
Workstations are part of the master data which needs to be set up in Carrier Connect. A workstation has assigned printers (usually for label printing and standard (general) printing. Based on the assigned printers, the output format (PDF, ZPLII, etc.) is determined.\
Without a workstation, Carrier Connect cannot prepare or print any data or documents.

## doCompletion

This is a simple true/false parameter indicating whether a shipment has been completed or whether further operations like adding more packages, items, etc. have been planned for it.\
Once a shipment has been completed, it can no longer be changed apart from canceling it.\
Only completed shipments can be assigned to pickups. If a carrier is set up with automatic pickup disposal, all completed shipments will be automatically assigned to a pickup.
