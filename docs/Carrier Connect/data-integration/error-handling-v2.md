---
title: Error Handling
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
If errors or warnings occur, the API response will always have header information indicating the type (error, retryable error, and/or warnings) and contains the related messages.

```json
{
  "hasErrors": true,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [
    {
      "messageType": "ERROR",
      "messageIdentCode": "PICKUP_NOT_FOUND_ERROR",
      "messageTexts": [
        {
          "languageISOCode": "en",
          "text": "Unable to find pickup for Pickup no. ..."
        }
      ],
      "indentationLevel": 0
    }
  ]
}
```
```xml XML
<hasErrors>true</hasErrors>
<hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
<hasWarnings>false</hasWarnings>
<messages>
	<messageType>ERROR</messageType>
	<messageIdentCode>PICKUP_NOT_FOUND_ERROR</messageIdentCode>
	<messageTexts>
		<languageISOCode>en</languageISOCode>
		<text>Unable to find pickup for Pickup no. ...</text>
	</messageTexts>
	<indentationLevel>0</indentationLevel>
</messages>
```

## hasErrors

An error is returned if the operation couldn't be performed because of a **basic issue** (non-unique transactionIds or if data cannot be found in the system, as in the example above). The shipment won't be created.

## hasOnlyRetryableErrors

If all errors are retryable errors, e.g. some data was locked, this is indicated.

## hasWarnings

A warning is returned if if the operation couldn't be performed because there is for example a missing field, a wrong postal code or the chosen carrier service is not available for the consignee. Usually the shipment will be created, but no labels (if requested) will be printed.

Note: At the moment, the `indentationLevel` is not used. It is always "0".

> ❗️ 
> 
> Be aware that **no shipment will be created** on a `createShipment` if you are using the following parameter combination: 
> 
> - `doCompletion = true` && 
> - `creationMode = VALIDATION_OK` 
> 
> And getting back only warnings: 
> 
> - `hasErrors = false` && 
> - `hasWarnings = true` 
> 
> Since a shipment can't be closed/completed (`doCompletion = true`) without the necessary label documents being created, in this special case you have to handle the warnings as if they where errors.