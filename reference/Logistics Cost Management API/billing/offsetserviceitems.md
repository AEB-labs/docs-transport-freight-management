---
title: offsetServiceItems
excerpt: >-
  Offset the service items in the Billing engine.<br> Offsetting a service item
  will offset all relevant settlement items of this service item, by creating
  exact copies of the relevant settlement items with reversed sign.<br>
  Depending on customizing, some settlement items will not take part in
  offsetting the service item and some settlement items will prevent any
  offsetting at all, which leads to an error.<br> The processing of all items
  will be done in one transaction, so in case of any error, nothing will be
  persisted. Therefore check the errorFlag and error message arrays in the
  response for any error to detect this case.<br>
api:
  file: logistics-cost-management-http-api.json
  operationId: offsetServiceItems
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---