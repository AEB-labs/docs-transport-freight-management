---
title: Printing documents
excerpt: 'ProcessParms: Knowing how to print'
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
      slug: referencing-data
      title: Referencing data
---
##Output modes
Creating documents like labels and loading list is an essential part of Carrier Connect.
Ideally, Carrier Connect simply creates all necessary documents and returns them in the response of the API call. If assynchronous communication is used, the documents can be retrieved at any time after creation using e.g. the sync API calls.

The way documents are printed can be determined by the *document output mode*:

**Output mode RETURN**
This is the preferred mode when working synchronously.
All requested documents will be returned in the response to the API call.
[block:code]
{
  "codes": [
    {
      "code": "...\n<documentOutputScope>\n  <scope>RETURN</scope>\n</documentOutputScope>\n...",
      "language": "xml"
    },
    {
      "code": "{ \n  ...\n   \"documentOutputScope\": {\n      \"scope\": \"RETURN\"\n    },\n  ...\n}",
      "language": "json"
    }
  ]
}
[/block]
**Output mode NONE**
No output will be generated. This is independent from the document generation itself. This parameter simply means that there will be no outpout of documents.
In more complex shipping scenarios, it can be useful to generate documents ahead of time and to request them for printing only at a later stage.
[block:code]
{
  "codes": [
    {
      "code": "...\n<documentOutputScope>\n  <scope>NONE</scope>\n</documentOutputScope>\n...",
      "language": "xml"
    },
    {
      "code": "{ \n  ...\n   \"documentOutputScope\": {\n      \"scope\": \"NONE\"\n    },\n  ...\n}",
      "language": "json"
    }
  ]
}
[/block]
**Output mode PRINT**
This is a special mode if the requesting ERP system has no own printing capabilities and works only in connection with an *AEB printing agent*.
Using this mode will result in print jobs assigned to the *workstation ID* used in the API call. The *AEB print agent* must run on the client system responsible for printing and constantly polls for print jobs using a specific *workstation ID*.
Note: This should not be the first choice for printing since printing performance is not as good as when using the *RETURN mode* and more information about the printing infrastructure e.g. the specific printers (not just the type of printers) must be provided in Carrier Connect.
[block:code]
{
  "codes": [
    {
      "code": "...\n<documentOutputScope>\n  <scope>PRINT</scope>\n</documentOutputScope>\n...",
      "language": "xml"
    },
    {
      "code": "{ \n  ...\n   \"documentOutputScope\": {\n      \"scope\": \"PRINT\"\n    },\n  ...\n}",
      "language": "json"
    }
  ]
}
[/block]