---
title: Shipment pre-validation
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
The call of <a href="https://carrierconnect.docs.developers.aeb.com/reference#validateshipment-1" target="_blank">validateShipment</a> provides the advantage of validating shipment data before a createShipment call will persist a shipment in the database.

There is no general answer what the validateShipment call will check beforehand. It is also good to know that the validateShipment will not be successful for all carriers. When the validateShipment call does not check anything or is not implemented yet, the response will be "The carrier does not support carrier-specific route validations."

Pre-validation checks if the shipment with the given carrier, service, and consignee (postal code and country validation) will receive a valid routing and will succeed when it comes to label printing.\
Only data on the shipment level will be considered without the packages, items, or hazardous goods. Thus, a successful validateShipment call will not necessarily lead to the successful printing of labels for a specific package.\
In most cases, package data influences checks as well e.g. package weight, dimensions, or quantity reglementation. The same applies to shipment items which are required for hazardous goods or shipping to third country. This will not be checked in the pre-validation. However, successful routing for the selected addresses and services will provide a useful indication to the carrier.

The important parameter in the request is the validation mode. Until now, only the "ROUTE\_SERVED" mode is supported.

```xml
<validationParms>
   <validationMode>ROUTE_SERVED</validationMode>
</validationParms>
```

For the response, there are several possible scenarios.

Potential validation results and their reasons:

"VALIDATION\_NO\_CHECK\_SELECTED" - No or invalid validation mode in the request.\
"VALIDATION\_FAILED" - Master data problem of the carrier configuration or route is not valid.\
"VALIDATION\_MISSING\_DATA" - Required data is missing in the request.\
"VALIDATION\_REQUEST\_NOT\_SUPPORTED" - Carrier does not support validateShipment or it is not implemented yet.\
"VALIDATION\_OK" - Validation was successful.
