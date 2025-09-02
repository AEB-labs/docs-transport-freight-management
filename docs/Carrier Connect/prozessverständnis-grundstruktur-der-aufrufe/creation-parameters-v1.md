---
title: 🔧 Creation Parameters (OLD)
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: pickup
      title: 🚚 Pickup processing
---
[block:html]
{
  "html": "<style>\n  span.cm-s-neo {\n    background-color: #f2f2f2;\n    color: red;\n  }\n</style>"
}
[/block]


# Creation Modes

Sometimes sending data to Carrier Connect doesn't work out as expected: e.g. the zip code is incorrect, the carrier doesn't allow to ship packages with these dimensions or not all required data is available.

These and many more validations are performed every time new shipments, packages, items, etc. are to be created.

Carrier Connect allows you to choose between various _creation modes_, which determine the behavior for data creation and error handling.

## Creation mode "ALWAYS": Shipment and packages are created, even if validation fails

The shipment and packages are created even if validation fails and validation warnings are returned. 

It is possible to configure Carrier Connect to respond with an "error label", which contains the error and/or warnings. This helps also to at least have "something" to be printed even if the real carrier label could not be created.

The errors can then be corrected 

- either manually using the Carrier Connect UI (attention: there will probably be a system inconsistency between Carrier Connect and the sending ERP / WMS system)
- in the sending system (ERP / WMS system). Then the shipment has to be canceled via the _cancelShipment_ API call and retransmitted with a _createShipment_ call. The cancellation step is necessary because a direct retransmission of existing shipments and packages is not allowed.

```json
... 
"creationParms": {
    "creationMode": "ALWAYS"
  },
...
```
```xml XML
<creationParms>
	<creationMode>ALWAYS</creationMode>
</creationParms>
```

## Creation mode "VALIDATION_OK": Shipments and packages are only created, if the shipment could be successfully validated

The shipments, packages, or items are only created if the shipment could be successfully validated. Otherwise, validation warnings will be returned in the response. A direct retransmission, after reviewing the data, is possible since no data has been created by the initial call.

```json
... 
"creationParms": {
    "creationMode": "VALIDATION_OK"
  },
...
```
```xml
<creationParms>
	<creationMode>VALIDATION_OK</creationMode>
</creationParms>
```

> 📘 What is common use?
> 
> Most customers prefer the "VALIDATION_OK" mode.