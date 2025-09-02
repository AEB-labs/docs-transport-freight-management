---
title: Requesting available carrier services
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
After you have found out which carriers are enabled for a specific client, a get request can be used to provide a list of all available master data like services, VAS (=value-added services), or additional values for one requested carrier.
The relevant request is called <a href="https://carrierconnect.docs.developers.aeb.com/reference#getcarrierproperties-1" target="_blank">getCarrierProperties</a>.

The request parameters are the same as in the 'Requesting available carriers' description, but here one additional parameter for the specific carrier named 'carrierIdentCode' must be given in the carrier properties.

A complete request looks as follows:
[block:code]
{
  "codes": [
    {
      "code": "<request>\n   <clientSystemId>SOAPUI</clientSystemId>\n   <clientIdentCode>ADMIN</clientIdentCode>\n   <userName>ADMIN</userName>\n   <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>\n   <carrierIdentCode>FEDEX</carrierIdentCode>\n</request>",
      "language": "xml"
    }
  ]
}
[/block]
The ident code of the carrier has to be exactly the same as defined in the master data of Carrier Connect.