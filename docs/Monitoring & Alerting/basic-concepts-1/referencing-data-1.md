---
title: Object IDs & References
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
In Monitoring & Alerting the logistics objects have an internal id that is used to uniquely identify each object.\
These ids are not prominently featured in the UI and differ from the ids a user might use to identify an object.\
For example, a Shipment has a *consignmentNumber* which is prominently displayed in the search and shipment overview and a *consignmentID*, which is used to internally identify an object.

*refXXX* fields are used to supply a reference to other objects by supplying their internal IDs.

## ID calculation (idRefScheme)

In the metadata DTO of the messages, you can specify an **idRefScheme** which determines how the internal IDs are generated and how given references are treated.

This field can be one of the following values:

## DEFAULT

By default the calculation will be identical to *SUPPLIER*.\
In some installations this behaviour may be overwritten (e.g. to behave like *BUYER*).\
This value is also used, when when the field 'idRefScheme' is empty.

## BUYER

The *BUYER* calculation scheme will calculate the id and reference numbers from functional data in the DTOs. It will preferably use buyer references when possible.

## SUPPLIER

The *SUPPLIER* calculation scheme will calculate the id and reference numbers from functional data in the DTOs. It will preferably use supplier references when possible.

## IDREFFIELDS

The *IDREFFIELDS* calculation scheme will calculate the id and reference numbers from the idXXX and refXXX fields in the DTOs. 

> 📘 Mandatory fields
>
> Using the scheme *IDREFFIELDS*, will make *idXXX* and *refXXX* fields become mandatory.

If a DTO has no idXXX field then the calculation of the field is not necessary.

## ID Calculation table

This table shows how the internal ID calculation is done for the different **idRefSchemes**.

![1371](https://files.readme.io/414afcc-ID-Kalkulationsschema.PNG "ID-Kalkulationsschema.PNG")

HINT: The references in items (shipment / order) to the parent object are always set implicitly by the parent, since the objects are always transferred together. The schemas can be changed in customer adaptions. Schema DEFAULT is not a separate schema, but uses the logic of schema SUPPLIER in the standard system. This can also be changed in customer adaptions.
