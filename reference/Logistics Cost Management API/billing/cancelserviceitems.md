---
title: cancelServiceItems
excerpt: >-
  Cancel the service items in the Billing engine.<br> Cancel a service item will
  try to logically remove the service item with all of its settelement items, if
  this is possible.<br> In some cases the cancellation of service items is not
  (or no longer) possible and will lead to errors.<br> E.g. the service item can
  not be found, or some of the settlement items of the service item can not or
  no longer be logically removed.<br> The processing of all items will be done
  in one transaction, so in case of any error, nothing will be persisted.
  Therefore check the errorFlag and message arrays in the response for any error
  to detect this case.<br>
api:
  file: logistics-cost-management-http-api.json
  operationId: cancelServiceItems
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---