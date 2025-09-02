---
title: Data validation and error handling
excerpt: 'CreationParms: Which creation mode fits best for you?'
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
      slug: prepare-and-output-scope
      title: Understanding data and document generation
---
## Creation Modes

Any data sent to Carrier Connect must be validated:\
Is the zip code correct? Does the carrier allow to ship packages with these dimensions? Is all required data available? These and many more checks are performed every time new shipments, packages, items, etc. are to be created.

Carrier Connect allows you to choose between various *creation modes* which determine the behavior for data creation and error handling.

### Creation mode "ALWAYS"

The shipment/packages is/are created even if validation fails and validation warnings are returned. Those warnings can either be corrected manually using the Carrier Connect UI or the shipment has to be canceled via the *cancelShipment* API call and retransmitted with a *createShipment* call. The cancellation step is necessary because a direct retransmission of existing shipments and packages is not allowed.\
In addition, it is possible to configure Carrier Connect to respond with an "error label" which contains the error and/or warnings. This helps also to at least have "something" to put on the package if the real carrier label could not be created.

```json
... 
"creationParms": {
    "creationMode": "ALWAYS"
  },
...
```

### Creation mode "VALIDATION\_OK"

The shipments, packages, or items are only created if the shipment could be successfully validated. Otherwise, validation warnings will be returned in the response. A direct retransmission, after reviewing the data, is possible since no data has been created by the initial call.

```json
... 
"creationParms": {
    "creationMode": "VALIDATION_OK"
  },
...
```

## Error handling

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
          "text": "Unable to find pickup for Pickup Pickup no. ..."
        }
      ],
      "indentationLevel": 0
    }
  ]
}
```

**hasErrors**\
An error is returned if the operation couldn't be performed because of a basic issue (non-unique transactionIds or if data cannot be found in the system, as in the example above).\
**hasOnlyRetryableErrors**\
If all errors are retryable errors, e.g. some data was locked, this is indicated.\
**hasWarnings**

Note: At the moment, the *indentationLevel* is not used. It is always "0".
