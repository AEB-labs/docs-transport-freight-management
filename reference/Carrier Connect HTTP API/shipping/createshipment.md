---
title: createShipment
excerpt: >-
  Creates a shipment with the data specified in the shipment request.<br> An
  error will be returned when the shipment exists already.<br> Optionally
  various operations like label preparation and label output can be applied on
  the shipment. A complete processing including the pickup assignment is also
  possible.<br> The operations are handled asynchronously, so operation
  processing errors and label documents are not part of the response. They can
  be retrieved with a <code>syncShipments</code> or <code>getShipments</code>
  call.
api:
  file: carrier-connect-http-api.json
  operationId: createShipment
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---