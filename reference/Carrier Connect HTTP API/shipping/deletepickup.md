---
title: deletePickup
excerpt: >-
  Cancels an existing pickup. All shipments are removed from the pickup and must
  be assigned to a new pickup by another <code>createPickup</code> call.<br>
  Warning: EDI data for the existing pickup might have already been sent to the
  carrier. So check with the carrier that it's fine to cancel the pickup and
  create a new (differing) one.
api:
  file: carrier-connect-http-api.json
  operationId: deletePickup
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---