---
title: Understanding data and document generation
excerpt: 'ProcessParms: Available preparation and output scopes'
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: Ways of communicating with Carrier Integration
  pages:
    - type: basic
      slug: synchron-or-asynchron
      title: Synchronous or asynchronous
---
##Preparation and output scopes
A distinct feature of Carrier Connect is the possibilty to separate the creation (generation) of documents completely from printing them.
This is done by setting the right *scope* for preparation and also for the desired output.

Of course, documents can be generated and requested for printing at the same time. This is easy and no problem!
However, it is also possible to split up the process and just generate documents and request them for printing later.
Sometimes it is also necessary to print or re-print documents for a specific package, rather than all documents for the complete shipment.

**Available scopes**
The following scopes can be used to determine what to "prepare" and what to "output":
**NONE**
No preparation and no output will happen. This is the default when scope is left empty.
**ALL**
All documents including the already processed ones are considered.
**REMAINING**
Only the remaining, not yet processed documents are considered.
**REQUEST**
Only documents for the packages included in the specific API call are considered.
**SHIPMENTONLY**
No package documents are processed. The shipment (header) is prepared. All possible calculations like routing data are calculated. This leads to improved performance when package documents are prepared.

**Example:**
Many of our customers use the following API calls to make use of this distinct feature:

*1) createShipment* (in order to create a shipment)
documentPrepareScope = SHIPMENTONLY
documentOutputScope = NONE
The shipment (header) data is validated and all necessary data is calculated e.g. routing date, tracking numbers on shipment level, etc. No output is generated.
[block:code]
{
  "codes": [
    {
      "code": " \"processParms\": {\n   ...\n    \"documentPrepareScope\": {\n      \"scope\": \"SHIPMENTONLY\"\n    },\n    \"documentOutputScope\": {\n      \"scope\": \"NONE\"\n    },\n    \"documentOutputMode\": {\n      \"mode\": \"NONE\"\n    },\n    \"doCompletion\": false\n  },\n",
      "language": "json"
    },
    {
      "code": "<processParms>\n  ...\n     <documentPrepareScope>\n         <scope>SHIPMENTONLY</scope>\n     </documentPrepareScope>\n     <documentOutputScope>\n         <scope>NONE</scope>\n     </documentOutputScope>\n     <documentOutputMode>\n         <mode>NONE</mode>\n     </documentOutputMode>\n  \t <doCompletion>false</doCompletion>\n</processParms>",
      "language": "xml"
    }
  ]
}
[/block]
*2) processShipment* (in order to add one or more packages)
documentPrepareScope = REQUEST
documentOutputScope = REQUEST
All data and documents related to the packages created in this specific request are calculated and prepared. The generated documents will be returned in the response to the API call.
[block:code]
{
  "codes": [
    {
      "code": " \"processParms\": {\n   ...\n    \"documentPrepareScope\": {\n      \"scope\": \"REQUEST\"\n    },\n    \"documentOutputScope\": {\n      \"scope\": \"REQUEST\"\n    },\n    \"documentOutputMode\": {\n      \"mode\": \"RETURN\"\n    },\n    \"doCompletion\": false\n  },\n",
      "language": "json"
    },
    {
      "code": "<processParms>\n  ...\n     <documentPrepareScope>\n         <scope>REQUEST</scope>\n     </documentPrepareScope>\n     <documentOutputScope>\n         <scope>REQUEST</scope>\n     </documentOutputScope>\n     <documentOutputMode>\n         <mode>RETURN</mode>\n     </documentOutputMode>\n  \t <doCompletion>false</doCompletion>\n</processParms>",
      "language": "xml"
    }
  ]
}
[/block]
*This example provides an ideal API workflow to optimize performance and data processing for label printing on the package level!*