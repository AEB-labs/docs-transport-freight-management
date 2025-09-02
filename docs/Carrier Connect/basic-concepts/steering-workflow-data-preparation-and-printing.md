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

##CreationParms
See [here](doc:data-validation-and-error-handling) for a detailed explanation.
[block:code]
{
  "codes": [
    {
      "code": "\"creationParms\": {\n    \"creationMode\": \"string\"\n  },",
      "language": "json"
    },
    {
      "code": " <creationParms>\n      <creationMode>?</creationMode>\n </creationParms>",
      "language": "xml"
    }
  ]
}
[/block]
##ProcessParms
Explantions for [processMode](doc:process-mode), [prepare and output scopes](doc:prepare-and-output-scope) and [output mode](doc:printing-modes) are available in the "Basic concepts" section.
[block:code]
{
  "codes": [
    {
      "code": " \"processParms\": {\n    \"processMode\": {\n      \"mode\": \"string\"\n    },\n    \"documentPrepareScope\": {\n      \"scope\": \"string\"\n    },\n    \"workstationId\": \"string\",\n    \"documentOutputScope\": {\n      \"scope\": \"string\"\n    },\n    \"documentOutputMode\": {\n      \"mode\": \"string\"\n    },\n    \"doCompletion\": true\n  },",
      "language": "json"
    },
    {
      "code": "<processParms>\n     <processMode>\n          <mode>?</mode>\n     </processMode>\n     <documentPrepareScope>\n          <scope>?</scope>\n     </documentPrepareScope>\n     <workstationId>?</workstationId>\n     <documentOutputScope>\n         <scope>?</scope>\n     </documentOutputScope>\n     <documentOutputMode>\n         <mode>?</mode>\n     </documentOutputMode>\n     <doCompletion>?</doCompletion>\n</processParms>",
      "language": "xml"
    }
  ]
}
[/block]
##Workstation ID
Most of the requests require a *Workstation ID*.
Workstations are part of the master data which needs to be set up in Carrier Connect. A workstation has assigned printers (usually for label printing and standard (general) printing. Based on the assigned printers, the output format (PDF, ZPLII, etc.) is determined.
Without a workstation, Carrier Connect cannot prepare or print any data or documents.

##doCompletion
This is a simple true/false parameter indicating whether a shipment has been completed or whether further operations like adding more packages, items, etc. have been planned for it.
Once a shipment has been completed, it can no longer be changed apart from canceling it.
Only completed shipments can be assigned to pickups. If a carrier is set up with automatic pickup disposal, all completed shipments will be automatically assigned to a pickup.