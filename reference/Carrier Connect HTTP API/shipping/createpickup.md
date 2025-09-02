---
title: createPickup
excerpt: >-
  Creates a new pickup for the shipments specified in the request.<br> Depending
  on the request, an error may be returned when the shipments can't form a
  single pickup, e.g. when they have different carriers.<br> Optionally the new
  pickup can be manifested. That means that the EDI is sent to the carrier if
  necessary and the pickup will be closed.<br> When specified in request, the
  manifest documents are printed.
api:
  file: carrier-connect-http-api.json
  operationId: createPickup
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---