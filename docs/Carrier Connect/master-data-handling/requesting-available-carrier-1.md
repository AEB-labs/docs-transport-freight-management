---
title: Requesting available carriers
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
Available carriers have to be configured correctly before starting to work with them and belong to the master data of Carrier Connect. Only enabled carriers can be used for shipping further on.

The <a href="https://carrierconnect.docs.developers.aeb.com/reference#getallcarriers-1" target="_blank">getAllCarriers</a> request returns the carriers that are available for the given client.
The request for the API call looks very similar to the first part of other requests and needs parameter like 'clientSystemId', 'clientIdentCode', 'userName', and 'resultLanguageIsoCodes'.

A complete request can be shown in the example below:
[block:code]
{
  "codes": [
    {
      "code": "<request>\n   <clientSystemId>SOAPUI</clientSystemId>\n   <clientIdentCode>ADMIN</clientIdentCode>\n   <userName>ADMIN</userName>\n   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>\n</request>",
      "language": "xml"
    }
  ]
}
[/block]