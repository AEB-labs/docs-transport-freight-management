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
## Overview

Monitoring & Alerting draws upon data from the various systems of all your supply chain partners and consolidates this data in one central location. This makes it possible to integrate all the participants of a logistics network.\
To do this the Monitoring & Alerting platform uses the following logistic objects.

![914](https://files.readme.io/0887abf-Draw-io_logistic_objects.png "Draw-io logistic objects.png")

## Order

An <Glossary>Order</Glossary> contains the information about a sale, it usually has a supplier and a buyer.

Some information a <Glossary>Order</Glossary> can contain:

* Sales & Purchase Number
* Customer
* Handover location
* Unloading location
* Order items

## Order item

An <Glossary>Order item</Glossary> contains information about a specific item that was ordered as part of an <Glossary>Order</Glossary>.

Some information a <Glossary>Order item</Glossary> can contain:

* Material
* Quantities
* Prices
* Conditions

## Shipment

> 📘 Consignment
>
> In the API shipments are usually called *Consignments*.

A <Glossary>Shipment</Glossary> contains information about goods that are transported from a shipping point to a consignee.\
Shipments are usually used to ship goods in order fulfill an order.

Some information a <Glossary>Shipment</Glossary> can contain:

* Consignee
* Shipping point
* Forwarder
* Shipment items
* Shipping units
* Transports

## Shipment item

> 📘 Consignment item
>
> In the API shipment items are usually called *Consignment items*.

A <Glossary>Shipment item</Glossary> contains information about a good that is part of a shipment.

## Shipping unit

> 📘 Handling Unit
>
> In the API shipping units are usually called *Handling units*.

A <Glossary>Shipping unit</Glossary> contains information about a physical shipping container that is part of shipment.\
For example this could be a carton, an EUR-pallet, an intermodal container...

## Transport

A <Glossary>Transport</Glossary> has the information about a transport that ships goods from A to B.\
For example this could be a ship that goes from Hamburg to Shenzhen or a truck that goes from Stuttgart to Munich.

A Shipment can consist of multiple transports, e.g. a truck transports the goods to the harbor and from there another transport with a ship is loaded.

Some information a <Glossary>Transport</Glossary> can contain:

* Start Location
* Destination Location
* Departure Dates (planned, expected, effected)
* Arrival Dates (planned, expected, effected)
* Means of Transport

## Physical Transport

Assuming two shipments are using the same transport from A to B, for example both were loaded onto the same truck at the ramp.\
A physical transport represents this transport by the carrier.

If a carrier sends an event, because the truck is delayed for example, it does not send multiple events. In this case the physical transport is updated from the message from the carrier, which then updates all the transports that are part of this physical transport, so the system knows multiple transports are now delayed.
