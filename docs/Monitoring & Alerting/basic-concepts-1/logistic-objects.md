---
title: Logistic Objects
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
  "title": "Overview"
}
[/block]
Monitoring & Alerting draws upon data from the various systems of all your supply chain partners and consolidates this data in one central location. This makes it possible to integrate all the participants of a logistics network. 
To do this the Monitoring & Alerting platform uses the following logistic objects.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0887abf-Draw-io_logistic_objects.png",
        "Draw-io logistic objects.png",
        914,
        1578,
        "#fafafa"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Order"
}
[/block]
An <<glossary:Order>> contains the information about a sale, it usually has a supplier and a buyer.

Some information a <<glossary:Order>> can contain:
- Sales & Purchase Number
- Customer
- Handover location
- Unloading location
- Order items
[block:api-header]
{
  "title": "Order item"
}
[/block]
An <<glossary:Order item>> contains information about a specific item that was ordered as part of an <<glossary:Order>>.

Some information a <<glossary:Order item>> can contain:
- Material
- Quantities
- Prices
- Conditions
[block:api-header]
{
  "title": "Shipment"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Consignment",
  "body": "In the API shipments are usually called *Consignments*."
}
[/block]
A <<glossary:Shipment>> contains information about goods that are transported from a shipping point to a consignee.
Shipments are usually used to ship goods in order fulfill an order.

Some information a <<glossary:Shipment>> can contain:
- Consignee
- Shipping point
- Forwarder
- Shipment items
- Shipping units
- Transports


[block:api-header]
{
  "title": "Shipment item"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Consignment item",
  "body": "In the API shipment items are usually called *Consignment items*."
}
[/block]
A <<glossary:Shipment item>> contains information about a good that is part of a shipment.


[block:api-header]
{
  "title": "Shipping unit"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Handling Unit",
  "body": "In the API shipping units are usually called *Handling units*."
}
[/block]
A <<glossary:Shipping unit>> contains information about a physical shipping container that is part of shipment.
For example this could be a carton, an EUR-pallet, an intermodal container...
[block:api-header]
{
  "title": "Transport"
}
[/block]
A <<glossary:Transport>> has the information about a transport that ships goods from A to B. 
For example this could be a ship that goes from Hamburg to Shenzhen or a truck that goes from Stuttgart to Munich.

A Shipment can consist of multiple transports, e.g. a truck transports the goods to the harbor and from there another transport with a ship is loaded.

Some information a <<glossary:Transport>> can contain:
- Start Location
- Destination Location
- Departure Dates (planned, expected, effected)
- Arrival Dates (planned, expected, effected)
- Means of Transport
[block:api-header]
{
  "title": "Physical Transport"
}
[/block]
Assuming two shipments are using the same transport from A to B, for example both were loaded onto the same truck at the ramp.
A physical transport represents this transport by the carrier.

If a carrier sends an event, because the truck is delayed for example, it does not send multiple events. In this case the physical transport is updated from the message from the carrier, which then updates all the transports that are part of this physical transport, so the system knows multiple transports are now delayed.