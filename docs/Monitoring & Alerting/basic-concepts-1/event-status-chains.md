---
title: Event & Status chains
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
[block:api-header]
{
  "title": "Status Chains"
}
[/block]
Status chains are used to configure the different status a logistic object can have.
The status chains are assigned by status chain filters, that can check for different values on the objects and then decide which status chain they should assign.
[block:callout]
{
  "type": "info",
  "title": "Different status chains",
  "body": "A shipment that is sent to another country, might need a status for *customs check in progress*, while a shipment that is sent within the same country does not need this status."
}
[/block]

[block:api-header]
{
  "title": "Event Chains"
}
[/block]
Event chains are used to map events to a corresponding status. Sending the event sets the status of the object.