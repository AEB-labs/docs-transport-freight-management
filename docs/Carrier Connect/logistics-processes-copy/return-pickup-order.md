---
title: Return / pickup order
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Clarification of terms

In Carrier Connect, inbound shipments (returns / pickup orders) can also be mapped for some carriers.

> 📘 The wording is often used analogously and the technical implementation is often similar, but technically there are differences.

## Pickup order

The goods are collected without an "outbound" shipment having previously existed. Example: Self-collection from the supplier or collection of goods for repair orders.

## Return

An "outbound" shipment has taken place, so the inbound shipment is a "retrieval" of the goods. As it is classically known from the private sector. We distinguish between returns "on demand" vs. "enclosed" ("Beileger").

## Returns "on demand" vs. "enclosed"

For returns, we again distinguish between two cases:

### Return "enclosed" (Beileger):

Every shipment prints two labels: the normal outbound label and the return label, which is enclosed in the package.

- This is often used in the B2C area or when it is known that this outbound shipment will also lead to a return (e.g. because the broken part is to be returned in the spare parts shipment).
- It is not certain that the return will actually take place. The carrier has not yet been commissioned.
- There is only one shipping order, the address constellation is that of the outbound.
- The "Enclosure" return is activated via an value added service (`shipment > valueAddedServices`in the `createShipment` call).

### Return "On demand":

Not every outbound shipment results in a return. The return must be explicitly ordered from the carrier and will therefore take place in any case.

- A separate shipping order is created for the inbound shipment.
- In this case, the goods recipient and pick-up point are "swapped" in comparison to the outbound - the address segment for the deviating pick-up address must be filled, the goods recipient is often analogous to the shipping point (or "goods receipt").
- A separate EDI is sent.
- Often no label is printed, because the label cannot physically reach the customer / pickup address. The driver then brings the label to the customer or prints it on site on his mobile printer. In exceptional cases (e.g. UPS "return service self-print", a PDF label is generated, which the customer can then send to the collection customer by e-mail)
- The technical implementation for returns "On demand" is thus analogous to the technical implementation for pickup creation and is therefore often used analogously.

# Comparison of Variants

|                                    | Pickup             | Return "On Demand"                                                                         | Return "Enclosed"  |
| :--------------------------------- | :----------------- | :----------------------------------------------------------------------------------------- | :----------------- |
| Outbound shipment occurs           | :x:                | :white_check_mark:                                                                         | :white_check_mark: |
| Inbound shipment definitely occurs | :white_check_mark: | :white_check_mark:                                                                         | :x:                |
| Separate shipping order needed     | :white_check_mark: | :white_check_mark:                                                                         | :x:                |
| "Reversal" of addresses necessary  | :white_check_mark: | :white_check_mark:                                                                         | :x:                |
| Separate label printing            | :x:                | Depends on the carrier. Usually no label printing, but possibly for e.g., UPS Self-Service | :white_check_mark: |