---
title: Master Data
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
This page explains the master data that is set up for the Swabian Clothing example.
[block:api-header]
{
  "title": "Order Status & Event chains"
}
[/block]
In this example we're using a simple three step status chain for our orders.
A newly created order, that has not received any events has the status `NEW`. After that it can have the status `Processed` which indicates that the order is done from our side (shipped to the customer).
`Fulfilled` indicates that the order was fulfilled.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/647d8d0-statuschain_order.PNG",
        "statuschain_order.PNG",
        741,
        90,
        "#bfdee9"
      ]
    }
  ]
}
[/block]
To set a order to the processed state send the `SHIPPED` event, to set it to fulfilled send the `DELIVERED` event.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/862c3be-events_order.PNG",
        "events_order.PNG",
        283,
        252,
        "#e8eaec"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Shipment Status & Event chains"
}
[/block]
In this example we're using a simple three step status chain for our Shipments.
A newly created shipment, that has not received any events has the status `Prepared`, we only create the shipment object once it is prepared. 
After that it can have the status `Shipped` which indicates that the shipment is out of our hands (shipped to the customer).
`Received` indicates that the carrier has delivered the shipment.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/670d610-statuschain_consignment.PNG",
        "statuschain_consignment.PNG",
        738,
        90,
        "#bfdee9"
      ]
    }
  ]
}
[/block]
## Propagations
Additionally we added propagations, so that a `Shipped` on the consignment also triggers the `Shipped` event on the corresponding order. The same goes for `Received`.
By doing so, we save duplicate calls to shipments and orders.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7e505b3-events_propagations.PNG",
        "events_propagations.PNG",
        596,
        278,
        "#d8e4e1"
      ]
    }
  ]
}
[/block]