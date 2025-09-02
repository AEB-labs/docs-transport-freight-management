---
title: Creating a shipment
excerpt: ''
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
      slug: add-packages
      title: Adding packages
---
[block:api-header]
{
  "title": "Everything starts with the shipment"
}
[/block]
Creating a shipment is the starting point for everything which can be accomplished within Carrier Connect.
Using <a href="https://carrierconnect.docs.developers.aeb.com/reference/api-overview#createshipment-1" target="_blank">createShipment</a> creates a shipment and returns a unique shipment number after successfully creating the shipment.
This shipment number can be used to reference the shipment when adding futher operations to the shipment later on.
[block:code]
{
  "codes": [
    {
      "code": " <result>\n       <hasErrors>false</hasErrors>\n       <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n       <hasWarnings>false</hasWarnings>\n   <shipmentNumber>0007544</shipmentNumber>\n        ...\n</result>\n",
      "language": "xml"
    }
  ]
}
[/block]
However, <a href="https://carrierconnect.docs.developers.aeb.com/reference/api-overview#createshipment-1" target="_blank"> createShipment</a> also allows to create a complete shipment with packages, items, etc., set the shipment to 'complete' and request all related documents within one call!
This provides a quick and easy process if all necessary data is available before creating the shipment.

**See also our SOAP Java documentation.**
[block:embed]
{
  "html": false,
  "url": "https://rz3.aeb.de/demo1cai/servlet/bf/doc/DLCarrierBF/de/aeb/xnsg/dl/bf/DLCreateShipmentResponseDTO.html",
  "title": "DLCreateShipmentResponseDTO (DespatchLight_ClientIF.3.0 20180118 API)",
  "favicon": null,
  "iframe": false
}
[/block]