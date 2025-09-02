---
title: Message Metadata
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
The Message Metadata is part of many API functions and determines fundamentally how the received message is to be interpreted by the system.
[block:api-header]
{
  "title": "updateMode"
}
[/block]
The *updateMode* tells the system how the received data should be inserted into the system.

## STANDARD
In the standard update mode the loaders will only write new contents to the fields of the corresponding object. No field content will be deleted.

If the main object of the message has any sub objects (e.g. a shipment can have shipment items) those sub object will be updated in the same way and if an existing sub object is not part of the message, it will not be deleted.

## STRUCTURE
In the structure update mode the loaders will write new contents to the fields of the corresponding object. No field contents will be deleted.

If the main object of the message has any sub objects (e.g. a shipment can have shipment items) those sub object will be updated in the same way BUT if an existing sub object is not part of the message, it will be deleted. 

## NOUPDATE
In the no-update update mode the loaders will check, if the corresponding object is already existent in the database.

If the object is in the database, nothing will be done.
If the object is NOT in the database, it will be loaded by standard means.


## DELETE

In this mode the loader will delete the main object of the message and all of its sub objects.
[block:api-header]
{
  "title": "Receiverrole & Senderrole"
}
[/block]
The role of the receiver of the message in the supply chain. This may be one of the constants *BUYER*, *SUPPLIER* or *FORWARDER*.

This will affect how the reference numbers (e.g. orderNumber, materialNumber) will be treated when inserting into the database.

## Examples of effects of receiverRole

### Shipment

**Affected field:**
Incoming shipment (isIncomingConsignment)

** receiverRole = BUYER:** 
isIncomingConsignment = True

** receiverRole = SUPPLIER:** 
isIncomingConsignment = False

** Info **
Depending on the point of view or partner, shipments are incoming or outgoing. If the recipient role is the buyer, then it is an **incoming shipment**. If the recipient is the vendor, then it is an **outbound shipment**. This field is currently for information purposes only and is not used in any logic. You can find it in the system folder of a delivery.

### Order
**Affected field:**
Incoming order
(isIncomingOrder)

** receiverRole = BUYER:** 
isIncomingOrder = False

** receiverRole = SUPPLIER:** 
isIncomingOrder = True

** Info **
Depending on the point of view or partner, orders are incoming or outgoing. Incoming orders are "purchase orders" from the point of view of the buyer and outgoing orders are "orders" from the point of view of the supplier. The field Inc. Order determines which order numbers are displayed in certain screens.

### All objects
**Affected field:**
Number from partners (partyNumber)

** receiverRole = BUYER:** 
partyNumber = dto.partyNumberBuyer

** receiverRole = SUPPLIER:** 
partyNumber = dto.partyNumberSupplier

** Info **
The field "Number" in the partners (CParty) is filled in the interface via the fields partyNumberBuyer, partyNumberSupplier and partyNumberForwarder in the corresponding DTO.
This should represent the usecase that a partner (e.g. forwarding agent) has a different number in the buyer's IT system than in the supplier's IT system. The numbers therefore represent the buyer's, vendor's or forwarding agent's view of the partner sent. Note: The partyNumberForwarder field is not taken into account when reading messages and therefore does not need to be filled.

### Items
**Affected fields:**
Material number
Product group

** receiverRole = BUYER:** 
materialNumberBuyer
productGroupBuyer

** receiverRole = SUPPLIER:** 
materialNumberSupplier
productGroupSupplier

** Info **
In the interface, there are 3 fields for the material number in items in substructure CLISMaterial: identCode (Material No.), identCodeBuyer (Material No. Buyer) and identCodeSupplier (Material No. Supplier).
When importing, the three fields are transferred 1:1 to the item. The system then checks which role the message recipient has and overwrites the value in material number with one of the other two values. The same applies to the product group.