---
title: Validate
excerpt: 'Learn how to validate shipment data before creating a shipping order:'
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

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/validateshipment" target="_blank">validateShipment</a> call provides the advantage of validating shipment data _before_ a `createShipment` call will persist a shipment in the database.

<Callout icon="📘" theme="info">
  * There is no general answer, what the `validateShipment` call will check beforehand. 
  * It is also good to know that the `validateShipment` will not be successful for all carriers. When the `validateShipment` call does not check anything or is not implemented yet, the response will be "The carrier does not support carrier-specific route validations."
</Callout>

# Pre-validation

Pre-validation checks, if the shipment with the given carrier, service, and consignee (postal code and country validation) will succeed when it comes to label printing.

> 🚧 What's not included in the pre-validation
>
> In most cases, package data influences checks as well e.g. package weight, dimensions, or quantity reglementation. The same applies to shipment items which are required for hazardous goods or shipping to third country. This will not be checked in the pre-validation. However, successful routing for the selected addresses and services will provide a useful indication to the carrier.

## Request parameters

The important parameter in the request is the validation mode. The different modes must be separated by `|` if more than one mode wants to be used, at the same time. **Don't use blanks before and after the `|`.**

Valid values are:

| Value             | Description                                                                                       |
| :---------------- | :------------------------------------------------------------------------------------------------ |
| ROUTE_SERVED      | Checks if a shipment can be sent to the consignee address with the specified carrier and service. |
| SERVICE_COMPLIANT | Checks if the shipment data are in compliance with the carriers requirements.                     |

```json
{
  "validationParms": {
    "validationMode": "ROUTE_SERVED|SERVICE_COMPLIANT"
  }
}
```
```xml
<validationParms>
   <validationMode>ROUTE_SERVED|SERVICE_COMPLIANT</validationMode>
</validationParms>
```

## Potential validation results and their reasons

For the response, there are several possible scenarios.

| Result                           | Reason                                                                  |
| :------------------------------- | :---------------------------------------------------------------------- |
| VALIDATION_NO_CHECK_SELECTED     | No or invalid validation mode in the request.                           |
| VALIDATION_FAILED                | Master data problem of the carrier configuration or route is not valid. |
| VALIDATION_MISSING_DATA          | Required data is missing in the request.                                |
| VALIDATION_REQUEST_NOT_SUPPORTED | Carrier does not support validateShipment or it is not implemented yet. |
| VALIDATION_OK                    | Validation was successful.                                              |
